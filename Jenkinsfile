pipeline {
    agent any

    environment {
        IMAGE_NAME = "oct-cicd-app"
        CONTAINER_NAME = "oct-cicd-container"
    }

    stages {
        stage('Pull Code') {
            steps {
                git branch: 'main', url: 'https://github.com/likithm617-rgb/oct-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                docker run -d --name $CONTAINER_NAME -p 3000:80 $IMAGE_NAME:latest
                '''
            }
        }
    }
}
