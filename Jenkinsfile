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
                bat '"C:/Users/DELL/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe" --version'
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
                bat '"C:/Users/DELL/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe" build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }
        stage('Run Container'){
            steps{
                bat '''
                    "C:/Users/DELL/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe" run -d --name node-app-%BUILD_NUMBER% -p %APP_PORT%:3000 %IMAGE_NAME%:%BUILD_NUMBER%
                '''
            }
        }
        stage('Verify'){
            steps{
                bat '''
                    echo APP Deployed Successfully
                    echo Open http://localhost:%APP_PORT%
                    "C:/Users/DELL/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe" ps
                '''
            }
        }
    }
}