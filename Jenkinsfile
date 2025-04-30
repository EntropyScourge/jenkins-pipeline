pipeline {
    agent any

    stages {
        stage ('Clean Up'){
            steps {
                echo 'Cleaning workspace...'
                deleteDir() // Clean up the workspace before starting the build
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here
                // dir('jenkins-pipeline') {
                //     // Assuming you have a build script in the cloned repo
                //     sh "chmod +x build.sh" // Make sure the script is executable
                // }
                // sh "cd jenkins-pipeline && ./build.sh"
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