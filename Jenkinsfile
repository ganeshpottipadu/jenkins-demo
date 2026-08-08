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
