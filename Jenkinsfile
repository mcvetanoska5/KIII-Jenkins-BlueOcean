node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        // Only build the Docker image if we're on the 'dev' branch
        if (env.BRANCH_NAME == 'dev') {
            app = docker.build("mcvetanoska5/kiii")
        } else {
            echo "Not on 'dev' branch. Skipping Docker build."
        }
    }
    stage('Push image') {
        // Only push the image if we're on the 'dev' branch
        if (env.BRANCH_NAME == 'dev') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        } else {
            echo "Not on 'dev' branch. Skipping Docker push."
        }
    }
}