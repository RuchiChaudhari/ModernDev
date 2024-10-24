pipeline {
    agent any
    environment {
        // Explicitly setting the Docker path
        PATH = "/usr/bin:/usr/local/bin:${env.PATH}" 
        DOCKER_USERNAME = 'ruchi563' // Your Docker username
        DOCKER_PASSWORD = 'abhiruchi1996' // Your Docker password
    }
    stages {
        stage('Clean and Clone Repository') {
            steps {
                cleanWs()
                sh 'git clone https://github.com/RuchiChaudhari/ModernDev.git'
            }
        }
        stage('List Files') {
            steps {
                dir('assignment9') {
                    sh 'ls -l'
                }
            }
        }
        stage('Build') {
            steps {
                dir('assignment9') {
                    // Ensure the Docker binary is found using the provided PATH
                    sh 'docker build -t ruchi563/assignment9 -f Dockerfile .'
                }
            }
        }
        stage('Login') {
            steps {
                // Use Docker path to ensure login happens correctly
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin docker.io'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push ruchi563/assignment9'
            }
        }
        stage('Run in Daemon Mode') {
            steps {
                sh 'docker rm -f my_container || true'
                sh 'docker run -d --name my_container ruchi563/assignment9'
            }
        }
    }
}
