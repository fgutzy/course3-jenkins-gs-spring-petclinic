pipeline {
    agent any
    
    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }
        stage("Test") {
            steps {
                bat "./mvnw test"
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
                  statusResultSource: [$class: 'DefaultStatusResultSource']])
        }
        failure {
            step([$class: 'GitHubCommitStatusSetter', 
                  reposSource: [$class: 'AnyDefinedRepositorySource'], 
                  contextSource: [$class: 'DefaultCommitContextSource'], 
                  statusResultSource: [$class: 'DefaultStatusResultSource']])
        }
    }
}
