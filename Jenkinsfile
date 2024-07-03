pipeline {
    agent any

    tools {
        nodejs "Node22.4" // The name you gave in the NodeJS configuration
    }

    environment {
        FASTLANE_LANE = "test"
        GIT_REPO_URL = "https://github.com/TruongMinhThuan/AwesomeProjectFastlane.git"
        GIT_BRANCH = "main"
    }


    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.GIT_BRANCH}", url: "${env.GIT_REPO_URL}"
            }
        }

        stage("Install Gems Locally") {
            steps {
                dir("ios") {
                    sh """
                    bundle config set --local path 'vendor/bundle'
                    bundle install
                    """ 
                }
            }
        }
        
        stage('Build and Upload to TestFlight') {
            steps {
                sh 'npm install'
                dir('ios') {
                    sh 'fastlane test'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and upload completed successfully!'
        }
        failure {
            echo 'Build or upload failed!'
        }
    }
}