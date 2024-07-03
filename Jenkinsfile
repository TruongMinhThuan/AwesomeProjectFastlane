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

                // Load RVM and use the correct Ruby version
                sh '''
                   source ~/.rvm/scripts/rvm
                   rvm use 3.3.3 --default
                   gem install bundler -v 3.3.3 --user-install
                   export PATH=$HOME/.gem/ruby/3.3.3/bin:$PATH
                '''
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