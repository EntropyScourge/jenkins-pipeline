pipeline {
    agent any

    stages {
        environment {
            ENV = 'DEV'
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
                // Add your build steps here
                sh "build.sh"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test steps here
                sh "test.sh"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deployment steps here
                sh "export JENKINS_NODE_COOKIE=do_not_kill ; bash scripts/deploy.sh"
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