pipeline {
    agent any
    
    stages{
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
            setGitHubCommitStatus state: 'SUCCESS', context: 'Jenkins Build', message: 'Build successful'
        }
        failure {
            setGitHubCommitStatus state: 'FAILURE', context: 'Jenkins Build', message: 'Build failed'
        }
    }
}

