pipeline {
  agent any

  environment {
    DOCKER_IMAGE = "barhaim10/the-last-jenkins-exercise"
    DOCKER_TAG = "latest"
    DOCKER_CREDENTIALS_ID = "dockerhub-creds" // את זה תגדירי ב-Jenkins ב-Manage Credentials
  }

  stages {
    stage('Clone Repo') {
      steps {
        git url: 'https://github.com/Bar-Haim/jenkins-freestyle-demo.git', branch: 'main'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
        }
      }
    }

    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
            docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
          }
        }
      }
    }

    stage('Run Container (optional)') {
      steps {
        sh "docker run -d --rm ${DOCKER_IMAGE}:${DOCKER_TAG}"
      }
    }
  }
}
