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
        stage('Initialize') {
            steps {
                slackSend color: "good", message: "Pipeline started for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
                echo 'Initializing pipeline...'
            }
        }
        stage('Scan secrets') {
            steps {
                slackSend color: "good", message: "Secret scanning started for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
                echo 'Scanning for secrets...'
                sh '''curl -LO https://github.com/gitleaks/gitleaks/archive/refs/tags/v8.25.1.tar.gz
                tar -xzf gitleaks-8.25.1.tar.gz
                ./gitleaks protect -v
                rm -rf gitleaks*
                '''
                // '''
                slackSend color: "good", message: "Secret scanning completed for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
            }
        }
        stage('Build') {
            steps {
                slackSend color: "good", message: "Build started for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
                echo 'Building...'
                // Add your build steps here
                sh "pwd"
                sh "bash scripts/build.sh"
                slackSend color: "good", message: "Build completed for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
            }
        }
        stage('Test') {
            steps {
                slackSend color: "good", message: "Tests started for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
                echo 'Testing...'
                // Add your test steps here
                sh "bash scripts/test.sh"
                slackSend color: "good", message: "Tests completed for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
            }
        }
        stage('Deploy') {
            steps {
                slackSend color: "good", message: "Deployment started for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
                echo 'Deploying...'
                // Add your deployment steps here
                sh "export JENKINS_NODE_COOKIE=do_not_kill ; bash scripts/deploy.sh"
                slackSend color: "good", message: "Deployment completed for ${env.JOB_NAME} - ${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME}"
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Add cleanup steps here
        }
        success {
            slackSend color: "good", message: "Pipeline succeeded on branch ${env.BRANCH_NAME}"
        }
    }
}