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
        },
        stage('Test SSH Connection') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: 'weather-nodejs-ec2-ssh',
                        keyFileVariable: 'SSH_KEY',
                        usernameVariable: 'SSH_USER'
                    )
                ]) {
                    sh '''
                        ssh -i "$SSH_KEY" \
                            -o BatchMode=yes \
                            -o StrictHostKeyChecking=yes \
                            "$SSH_USER@13.50.244.236" \
                            "echo 'SSH connection successful!' && whoami && hostname"
                    '''
        }
    }
}
    }
}
