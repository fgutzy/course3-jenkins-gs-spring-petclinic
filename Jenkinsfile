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
            step([$class: 'GitHubCommitStatusSetter', 
                  reposSource: [$class: 'AnyDefinedRepositorySource'], 
                  contextSource: [$class: 'DefaultCommitContextSource'], 
                  statusResultSource: [$class: 'ConditionalStatusResultSource', 
                                      results: [[buildStatus: 'SUCCESS', state: 'success']]]])
        }
        failure {
            step([$class: 'GitHubCommitStatusSetter', 
                  reposSource: [$class: 'AnyDefinedRepositorySource'], 
                  contextSource: [$class: 'DefaultCommitContextSource'], 
                  statusResultSource: [$class: 'ConditionalStatusResultSource', 
                                      results: [[buildStatus: 'FAILURE', state: 'failure']]]])
        }
    }
}
