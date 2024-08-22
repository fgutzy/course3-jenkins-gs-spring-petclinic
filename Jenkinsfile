pipeline {
    agent any
    
    stages{
        stage("checkout") {
            steps{
                git branch:'main', url: 'https://github.com/fgutzy/course3-jenkins-gs-spring-petclinic'
            }
        }
        stage("build"){
            steps {
                sh "mvn package"
            }
        }
        stage("capture"){
            steps {
                archiveArtifacts '**/target/*.jar'
            }
        }
        stage("testResults"){
            steps{
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
            }
        }
        stage("codeCoverage"){
            steps{
                jacoco()
            }
        }
    }
    post {
        always {
            echo "finally"
        }
    }
}

