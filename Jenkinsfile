pipeline {
    agent any

    environment {
        FASTLANE_LANE = "beta"
        GIT_REPO_URL = "https://github.com/TruongMinhThuan/AwesomeProjectFastlane.git"
        GIT_BRANCH = "main"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.GIT_BRANCH}", url: "${env.GIT_REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'bundle install'
            }
        }

        stage('Build and Upload to TestFlight') {
            steps {
                sh 'bundle exec fastlane ${FASTLANE_LANE}'
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