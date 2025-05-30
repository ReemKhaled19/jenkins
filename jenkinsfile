pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'reemsolimman/lab1'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ReemKhaled19/jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'a6865cf0-77a0-4d6c-8b47-6b8d83cd44cf', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'a6865cf0-77a0-4d6c-8b47-6b8d83cd44cf') {
                            dockerImage.push('latest')
                        }
                    }
                }
            }
        }
    }
}
