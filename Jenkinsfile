pipeline {
    agent {
        label 'test-server'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-demo:latest .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh 'docker stop jenkins-demo || true'
                sh 'docker rm jenkins-demo || true'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d --name jenkins-demo -p 8080:80 jenkins-demo:latest'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
                sh 'curl -I http://localhost:8080'
            }
        }
    }
}
