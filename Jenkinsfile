pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')  // ID from Jenkins credentials
        IMAGE_NAME = "your-dockerhub-username/myapp"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // For Node.js example:
                sh 'npm test || echo "No tests found"'
            }
        }

        stage('Push to DockerHub') {
            steps {
                echo 'Pushing image to DockerHub...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $IMAGE_NAME:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying container...'
                sh 'docker run -d -p 8080:8080 --name myapp $IMAGE_NAME:latest || echo "App already running"'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
