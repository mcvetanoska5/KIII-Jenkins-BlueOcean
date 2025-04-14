pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'dev') {
                        echo 'Building Docker image because we are on the dev branch.'
                        sh 'docker build -t mcvetanoska5/kiii .'
                    } else {
                        echo 'Not the dev branch, skipping Docker build.'
                    }
                }
            }
        }
        stage('Push to Docker Hub') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    echo 'Pushing Docker image to Docker Hub...'
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push mcvetanoska5/kiii'
                }
            }
        }
    }
}
