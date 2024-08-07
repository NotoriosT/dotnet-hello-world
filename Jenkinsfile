pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
        DOCKER_IMAGE = 'seu-usuario/dotnet-hello-world'
        REGISTRY_URL = 'https://index.docker.io/v1/'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/seu-usuario/dotnet-hello-world.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry("${REGISTRY_URL}", "${DOCKER_CREDENTIALS_ID}") {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook playbook: '/etc/ansible/playbooks/playbook-deploy.yml', inventory: '/etc/ansible/hosts'
            }
        }
    }
}
