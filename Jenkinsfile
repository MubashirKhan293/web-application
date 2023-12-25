pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Running the Python script...'
                bat 'python hello.py'
            }
        }
    }
}
