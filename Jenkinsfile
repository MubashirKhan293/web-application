pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo "=== Building Docker Image ==="
                    
                    // Use Docker Hub credentials from Jenkins Credential Store
                    withCredentials([usernamePassword(credentialsId: 'Mnop1234.', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                        sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                        sh "docker build -t mubashirkhan283/terminal_task:exam ."
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                 echo "=== Testing Docker Image ==="
                    // Use any testing tool for Flask (e.g., pytest)
                    sh "pip install -r requirements.txt"
                    sh "pytest tests/"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "=== Deploying Docker Image ==="
                    // Use Docker Hub credentials from Jenkins Credential Store
                    withCredentials([usernamePassword(credentialsId: 'Mnop1234.', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                        sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                        sh "docker push mubashirkhan283/terminal_task:exam"
                        // Other deployment steps...
                    }
                }
            }
    }

     post {
        failure {
            echo "=== Deployment Failed ==="
            echo "Rolling back to the previous version..."

            // Pull the previous Docker image and redeploy
            script {
                 sh "docker pull mubashirkhan283/terminal_task:latest"
                // Redeploy using your deployment strategy (e.g., Docker Compose)
                sh "docker-compose up -d"
            }

            echo "Rollback complete."
            echo "Sending email notification..."
            
            // Add additional steps as needed for notification or cleanup
             emailext subject: 'Flask App Deployment Failed',
                      body: 'The deployment of the Flask app has failed. Please check the Jenkins job for details.',
                      to: 'mbshrkhan123@gmail.com'
        }
    }
}
