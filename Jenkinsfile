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

        stage('Build & Test') {
            steps {
                // We use 'docker build' instead of 'npm install' because 
                // the Dockerfile handles all dependencies (including sqlite3)
                sh "docker build -t ${DOCKER_USER}/${APP_NAME}:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // This ID must match the one you created in Jenkins -> Credentials
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                    sh "docker push ${DOCKER_USER}/${APP_NAME}:latest"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to VM....'
                // This is where you would put your 'docker run' command for the VM
            }
        }
    }
}