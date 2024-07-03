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

     
        stage('Setup RVM and Ruby') {
            steps {

                sh 'npm install'

                  // Load RVM
                sh 'source $HOME/.rvm/scripts/rvm'
                
                // Use a specific Ruby version, for example, Ruby 2.7.1
                sh 'rvm use 2.7.1'
                
                // Install Node.js dependencies
                sh 'npm install'

                sh 'gem install cocoapods'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
                // Install Ruby gems using Bundler
                sh 'bundle install'
            }
        }

        stage('Install Pods') {
            steps {
                dir('ios') {
                    sh 'pod install'
                }
            }
        }

        stage('Build and Upload to TestFlight') {
            steps {
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