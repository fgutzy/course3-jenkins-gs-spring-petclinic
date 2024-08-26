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
        githubNotify context: 'Jenkins Build', description: 'Build successful', status: 'SUCCESS'
        }
        failure {
            githubNotify context: 'Jenkins Build', description: 'Build failed', status: 'FAILURE'
        }
    }
}
