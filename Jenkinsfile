node {
    // maven versi 3.9.8
    env.MAVEN_HOME="${tool 'maven'}"
    env.PATH="${env.MAVEN_HOME}/bin:${env.PATH}"
    def mvnHome = tool 'maven'
    stage('Build') {        
        sh "mvn -B -DskipTests clean package"
    }
    stage('Test') {
        sh "mvn test"
    }
}