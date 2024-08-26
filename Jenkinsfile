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
         stage("capture"){
            steps {
                archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
