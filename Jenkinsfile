pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    DOCKER_REGISTRY_URL = 'docker.io'
    DOCKER_IMAGE_NAME = "my-docker-image:${env.BUILD_NUMBER}"
  }

  stages {
    stage('Checkout') {
      steps {
        // Checkout the code from your repository
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          // Build Docker image
          def dockerImage = docker.build("my-docker-image:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Push Docker Image') {
        steps {
          script {
              // Authenticate with Docker Hub
              docker.withRegistry(DOCKER_REGISTRY_URL, DOCKERHUB_CREDENTIALS) {
                // Push Docker image to Docker Hub
                dockerImage.push(DOCKER_IMAGE_NAME)
              }
          }
      }
    }
  }
}
