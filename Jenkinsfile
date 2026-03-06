pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = "PavanBand"
        IMAGE_NAME = "pavanband/school-erp-devops"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/PavanBand/school-erp-devops.git'
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
                    credentialsId: 'dockerhub',
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {

                    sh 'docker login -u $USERNAME -p $PASSWORD'
                    sh 'docker tag $IMAGE_NAME $DOCKERHUB_USERNAME/school-erp-devops:latest'
                    sh 'docker push $DOCKERHUB_USERNAME/school-erp-devops:latest'
                }
            }
        }

    }
}
