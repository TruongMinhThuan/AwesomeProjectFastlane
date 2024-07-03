pipeline {
    agent any

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
            dir('ios') {
                steps {
                    sh 'fastlane ${FASTLANE_LANE}'
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