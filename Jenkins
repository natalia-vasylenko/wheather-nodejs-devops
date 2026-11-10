pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Project') {
            steps {
                sh '''
                    echo "Checking WeatherForecast repository..."
                    ls -la
                    test -f package.json
                    test -f Dockerfile
                    test -f docker-compose.yml
                '''
            }
        }
    }
}
