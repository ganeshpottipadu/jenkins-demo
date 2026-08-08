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

        stage('Build') {
            steps {
                sh 'echo "Building application..."'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                sh 'cat index.html'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Application deployed successfully!"'
            }
        }
    }
}
