pipeline {
    agent any

    environment {
        IMAGE_NAME = 'barhaim10/the-last-jenkins-exercise'
        IMAGE_TAG = 'latest'
        DOCKER_CREDS = 'docker-hub-creds'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDS}", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                }
            }
        }
    }
}
