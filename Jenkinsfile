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
                sh "docker build -t jenkins-demo:${BUILD_NUMBER} ."
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
                sh "docker run -d --name jenkins-demo -p 8080:80 jenkins-demo:${BUILD_NUMBER}"
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    echo "Checking application health..."

                    for i in {1..10}; do
                        if curl -f http://localhost:8080; then
                            echo "Application is healthy!"
                            exit 0
                        fi

                        echo "Application not ready yet... retrying"
                        sleep 3
                    done

                    echo "Application health check failed!"
                    exit 1
                '''
            }
        }
    }
}
