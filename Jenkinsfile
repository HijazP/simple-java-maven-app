node {
    // maven versi 3.9.8
    env.MAVEN_HOME="${tool 'maven'}"
    env.PATH="${env.MAVEN_HOME}/bin:${env.PATH}"
    stage('Build') {        
        sh "mvn -B -DskipTests clean install"
    }
    stage('Test') {
        sh "mvn test"
    }
    stage('Docker Build') {
        docker.build("hijaz/submisi-cicd-dicoding:latest", ".")
    }
    stage('Manual Approval') {
        input message: "Lanjutkan ke tahap Deploy?"
    }
    stage('Deploy') {
        sh "./jenkins/scripts/deliver.sh"
        echo "Jeda eksekusi pipeline selamat 1 menit"
        sh "sleep 1m"
    }
}