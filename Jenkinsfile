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
                  statusResultSource: [$class: 'ConditionalStatusResultSource', 
                                      results: [[buildStatus: 'SUCCESS', state: 'success', message: 'Build succeeded']]]])
        }
        failure {
            step([$class: 'GitHubCommitStatusSetter', 
                  reposSource: [$class: 'AnyDefinedRepositorySource'], 
                  contextSource: [$class: 'DefaultCommitContextSource'], 
                  statusResultSource: [$class: 'ConditionalStatusResultSource', 
                                      results: [[buildStatus: 'FAILURE', state: 'failure', message: 'Build failed']]]])
        }
    }
}
