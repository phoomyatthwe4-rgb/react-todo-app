pipeline {
    agent any

    tools {
        // This MUST match the name 'docker' you gave in Manage Jenkins -> Tools
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

        stage('Build Docker Image') {
            steps {
                script {
                    // This finds where Jenkins installed Docker and makes it usable
                    def dockerHome = tool name: 'docker', type: 'dockerTool'
                    withEnv(["PATH+DOCKER=${dockerHome}/bin"]) {
                        sh "docker build -t ${DOCKER_USER}/${APP_NAME}:latest ."
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    def dockerHome = tool name: 'docker', type: 'dockerTool'
                    withEnv(["PATH+DOCKER=${dockerHome}/bin"]) {
                        // Ensure you created 'docker-hub-creds' in Jenkins -> Credentials
                        withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                            sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                            sh "docker push ${DOCKER_USER}/${APP_NAME}:latest"
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Successfully built and pushed ${DOCKER_USER}/${APP_NAME}:latest"
                echo "Now you can run this on your VM!"
            }
        }
    }
}