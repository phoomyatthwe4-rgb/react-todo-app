pipeline {
    agent any

    tools {
        // Use 'dockerTool' because your Jenkins version requires this specific name
        dockerTool 'docker' 
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
        
        // ... (rest of your stages stay the same)
    }
}