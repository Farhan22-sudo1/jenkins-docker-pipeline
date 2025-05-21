pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerhub-credentials') // Set this ID in Jenkins Credentials
        IMAGE_NAME = 'farhan221/myapp'
        IMAGE_TAG = 'latest'
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
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Docker Login') {
            steps {
                echo 'Logging into Docker Hub...'
                sh '''
                    echo "$DOCKER_CREDENTIALS_PSW" | docker login -u "$DOCKER_CREDENTIALS_USR" --password-stdin
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
            }
        }
    }

    post {
        always {
            echo '✅ Jenkins Docker pipeline complete.'
        }
    }
}
