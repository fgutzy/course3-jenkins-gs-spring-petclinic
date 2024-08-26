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
        always {
            echo "finally"
        }
    }
}

