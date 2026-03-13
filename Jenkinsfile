pipeline {
    agent any

    environment {
        // Change this to YOUR Docker Hub ID
        DOCKER_USER = "phoomyatthwe6611"
        APP_NAME = "todo-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                // This will now use the Docker installed on your Mac/Server
                sh "docker build -t ${DOCKER_USER}/${APP_NAME}:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Ensure you have created 'docker-hub-creds' in Jenkins -> Credentials
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                    sh "docker push ${DOCKER_USER}/${APP_NAME}:latest"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Successfully built and pushed ${DOCKER_USER}/${APP_NAME}:latest"
                echo "Deployment step can go here."
            }
        }
    }
}