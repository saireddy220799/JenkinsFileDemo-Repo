pipeline{
    agent any

    parameters{
        string(
        name:'APP_PORT',
        defaultValue:'3000',
        description:'Server Port'
        )
    }
    environment{
        IMAGE_NAME='Jenkins-Demo-App'
    }
    stages{
        stage('Git Checkout'){
            steps{
                echo 'Checking out Source Code From Git Repo'
                checkout scm
            }
        }
        stage('Check Docker'){
            steps{
                bat 'decker --version'
            }
        }
        stage('Dependencies'){
            steps{
                bat 'npm install'
            }
        }
        stage('Test APP'){
            steps{
                bat 'npm test'
            }
        }
        stage('Build'){
            steps{
                bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }
        stage('RUn Container'){
            steps{
                bat '''
                    docker run -d --name node-app-%BUILD_NUMBER% -p %APP_PORT%:3000 %IMAGE_NAME%:%BUILD_NUMBER%
                '''
            }
        }
        stage('Verify'){
            steps{
                bat '''
                    echo APP Deployed Successfully
                    echo Open http://localhost:%APP_PORT%
                    docker ps
                '''
            }
        }
    }
}