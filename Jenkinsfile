pipeline {
    agent any

    tools {
        docker 'docker' // This connects to the tool you named 'docker' in Jenkins settings
    }

    environment {
        DOCKER_USER = "phoomyatthwe6611"
        APP_NAME = "todo-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh "docker build -t ${DOCKER_USER}/${APP_NAME}:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // IMPORTANT: Ensure you have created credentials in Jenkins 
                // with the ID 'docker-hub-creds'
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                    sh "docker push ${DOCKER_USER}/${APP_NAME}:latest"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to VM....'
            }
        }
    }
}