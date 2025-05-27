pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'farhan221/myapp:latest'
        DOCKER_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning GitHub repo...'
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t $DOCKER_IMAGE ."
            }
        }

        stage('Docker Login') {
            steps {
                echo 'Logging in to Docker Hub...'
                sh "echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin"
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing Docker image...'
                sh "docker push $DOCKER_IMAGE"
            }
        }
    }

    post {
        always {
            echo '✅ Jenkins Docker pipeline complete.'
        }
    }
}
