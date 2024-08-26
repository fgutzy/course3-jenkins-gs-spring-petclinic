pipeline {
    agent any
    
    stages {
        stage("Checkout") {
            steps {
                checkout scm
                sh 'env'  // Print all environment variables
                sh 'which nohup'  // Check if nohup exists and where it's located
                sh 'type nohup'   // On Unix systems, this shows the definition of nohup if it's a shell alias or function
            }
        }
        stage("Test") {
            steps {
                sh "mvn test"
            }
        }
        stage("Test Results") {
            steps {
                junit testResults: '**/target/surefire-reports/TEST*.xml'
            }
        }
    }
    post {
        success {
            step([$class: 'GitHubCommitStatusSetter', 
                  reposSource: [$class: 'AnyDefinedRepositorySource'], 
                  contextSource: [$class: 'DefaultCommitContextSource'], 
                  statusResultSource: [$class: 'DefaultStatusResultSource', status: 'SUCCESS']])
        }
        failure {
            step([$class: 'GitHubCommitStatusSetter', 
                  reposSource: [$class: 'AnyDefinedRepositorySource'], 
                  contextSource: [$class: 'DefaultCommitContextSource'], 
                  statusResultSource: [$class: 'DefaultStatusResultSource', status: 'FAILURE']])
        }
    }
}
