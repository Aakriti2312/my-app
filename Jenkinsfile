pipeline {
    agent any

    environment {
        IMAGE_NAME = "aakritidhawan/myapp"
    }

    stages {

        stage('Clone Source') {
            steps {
                echo "Cloning GitHub repository..."
                git branch: 'main', url: 'https://github.com/Aakriti2312/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                echo "Logging into Docker Hub..."
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh '''
                    echo $DOCKER_TOKEN | docker login -u aakritidhawan --password-stdin
                    '''
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully 🎉"
        }
        failure {
            echo "Pipeline failed ❌ Check logs"
        }
    }
}