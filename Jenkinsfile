pipeline {
    agent any

    environment {
            ENV = "${env.BRANCH_NAME == 'master' ? 'PROD' : 'DEV'}"
            BRANCH = "${env.BRANCH_NAME}"
            LANG = "en_US.UTF-8"
        }

    tools { go 'go-1.24' }

    stages {
        // stage ('Clean Up'){
        //     steps {
        //         echo 'Cleaning workspace...'
        //         deleteDir() // Clean up the workspace before starting the build
        //     }
        // }
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build steps here
                sh "pwd"
                sh "bash scripts/build.sh"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test steps here
                sh "bash scripts/test.sh"
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