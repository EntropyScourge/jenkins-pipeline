pipeline {
    agent any

    stages {
        environment {
            // Define any environment variables here
            ENV = 'PROD'
        }
        stage ('Clean Up'){
            steps {
                echo 'Cleaning workspace...'
                deleteDir() // Clean up the workspace before starting the build
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh "build.sh"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test steps here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deployment steps here
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Add cleanup steps here
        }
    }
}