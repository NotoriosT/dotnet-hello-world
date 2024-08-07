pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'dotnet-hello-world'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/NotoriosT/dotnet-hello-world.git', branch: 'main', credentialsId: 'github-token'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }
    }
}
