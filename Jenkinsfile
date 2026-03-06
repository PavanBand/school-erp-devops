pipeline {
    agent any

    environment {
        IMAGE_NAME = "pavanbandi07/school-erp-devops"
        CONTAINER_NAME = "school-erp-test"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                credentialsId: 'github-credentiales',
                url: 'https://github.com/PavanBand/school-erp-devops.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'cd backend && npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Run Container Test') {
            steps {
                bat 'docker run -d --name %CONTAINER_NAME% -p 5000:5000 %IMAGE_NAME%'
                powershell 'Start-Sleep -Seconds 10'
                bat 'curl http://localhost:5000/health'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker push %IMAGE_NAME%'
                }
            }
        }

        stage('Cleanup') {
            steps {
                bat 'docker stop %CONTAINER_NAME%'
                bat 'docker rm %CONTAINER_NAME%'
            }
        }
    }
}
