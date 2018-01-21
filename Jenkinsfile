pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
            args '-v /var/jenkins_home:/var/jenkins_home'
            args '--no-cache'
        }
    }
    stages {
        stage('Build') {
            notifyBuildStatus('STARTED')
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    }
    notifyBuildStatus(currentBuild.result)
}

def notifyBuildStatus(String buildStatus = 'STARTED') {
    // build status of null means successful
    buildStatus =  buildStatus ?: 'SUCCESSFUL'

    // Default values
    def colorName = 'RED'
    def colorCode = '#FF0000'
    def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
    def summary = "${subject} (${env.BUILD_URL})"
    def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
    <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>"""

    mail bcc: '', body: details, cc: '', from: '', replyTo: '', subject: 'Build status', to: 'pvsk1919@gmail.com'


}
