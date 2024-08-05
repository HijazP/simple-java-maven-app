node {
    // maven versi 3.9.8
    checkout scm
    env.MAVEN_HOME="${tool 'maven'}"
    env.PATH="${env.MAVEN_HOME}/bin:${env.PATH}"
    stage('Build') {        
        sh "mvn package"
    }
    stage('Test') {
        sh "mvn test"
    }
    stage('Docker Build') {
        docker.build("hijazp/spring-web-demo:latest", ".")
    }
    stage('Push Docker Image') {
        withCredentials([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            sh "docker login --username=$USERNAME --password=$PASSWORD"
            sh "docker push hijazp/spring-web-demo:latest"
        }
    }
    stage('Manual Approval') {
        input message: "Lanjutkan ke tahap Deploy?"
    }
    stage('Deploy') {
        sh 'ssh admin@18.136.208.216 "sudo docker run -d --name spring-boot-web --publish 80:8080 hijazp/spring-web-demo:latest"'
        echo "Jeda eksekusi pipeline selamat 1 menit"
        sh "sleep 1m"
    }
}