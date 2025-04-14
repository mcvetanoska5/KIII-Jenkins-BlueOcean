pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
          app = docker.build(DOCKER_IMAGE)
        }

      }
    }

    stage('Push image') {
      steps {
        script {
          docker.withRegistry(REGISTRY, DOCKER_CREDENTIALS) {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
          }
        }

      }
    }

  }
  environment {
    DOCKER_IMAGE = 'mcvetanoska5/kiii'
    REGISTRY = 'https://registry.hub.docker.com'
    DOCKER_CREDENTIALS = 'dockerhub'
  }
}