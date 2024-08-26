pipeline {
    agent any
    
    stages {
        stage("Checkout") {
            steps {
                checkout scm
                bat 'echo hello world'  // Print all environment variables
             }
        }
    }
}
