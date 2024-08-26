pipeline {
    agent any
    
    stages {
        stage("Checkout") {
            steps {
                checkout scm
                sh 'echo hello world'  // Print all environment variables
             }
        }
    }
}
