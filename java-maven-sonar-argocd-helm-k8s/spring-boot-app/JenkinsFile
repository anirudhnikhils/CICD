pipeline {
    agent any  // Use any available agent

    environment {
        REGISTRY_CREDENTIALS = credentials('docker-cred')  // Load credentials
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    echo 'Checkout stage passed'
                    checkout([$class: 'GitSCM',
                        branches: [[name: 'main']],
                        userRemoteConfigs: [[url: 'https://github.com/anirudhnikhils/CICD']]
                    ])
                }
            }
        }
        stage('Verify Dockerfile') {
            steps {
                script {
                    echo 'Verifying Dockerfile exists'
                    bat 'if not exist Dockerfile echo Dockerfile not found && exit 1'
                }
            }
        }
        stage('Build and Package') {
            steps {
                script {
                    echo 'Building and Packaging the application'
                    bat 'docker build -t your-app-image1:latest -f Dockerfile .'  // Ensure correct Dockerfile name
                }
            }
        }
        stage('Docker Login and Push') {
            steps {
                script {
                    echo 'Logging in and pushing the Docker image'
                    bat """
                        docker login -u ${env.REGISTRY_CREDENTIALS_USR} -p ${env.REGISTRY_CREDENTIALS_PSW}
                        docker push your-app-image1:latest  // Replace with your Docker image name
                    """
                }
            }
        }
    }
}
