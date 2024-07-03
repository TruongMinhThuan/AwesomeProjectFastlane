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

        stage('Build and Upload to TestFlight') {
            steps {
                sh 'yarn'
                dir('ios') {
                    sh 'bundle exec pod install'
                    sh 'bundle exec fastlane test'
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