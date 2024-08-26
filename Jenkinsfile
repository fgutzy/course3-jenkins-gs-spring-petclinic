pipeline {
    agent any
    
    stages{
        stage("Checkout") {
            steps {
                checkout scm
            }
        }
        stage("test"){
            steps {
                sh "mvn test"
            }
        }
        stage("testResults"){
            steps{
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
            }
        }
    }
    post {
        success {
            setGitHubCommitStatus context: 'Jenkins Build',
                                  description: 'Build successful',
                                  state: 'SUCCESS'
        }
        failure {
            setGitHubCommitStatus context: 'Jenkins Build',
                                  description: 'Build failed',
                                  state: 'FAILURE'
        }
    }
}
