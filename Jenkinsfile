pipeline {
    agent any

    environment {
        IMAGE_NAME = "pavanbandi07/school-erp-devops"
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
                sh 'npm install --prefix backend'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container Test') {
            steps {
                sh 'docker run -d -p 5000:5000 $IMAGE_NAME'
                sh 'sleep 10'
                sh 'curl http://localhost:5000/health'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }

        stage('Cleanup') {
            steps {
                sh 'docker stop $(docker ps -q) || true'
            }
        }

    }
}
