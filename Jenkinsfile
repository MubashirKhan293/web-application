pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
    }
}
