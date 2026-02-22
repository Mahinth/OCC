pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Python') {
            steps {
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y python3
                '''
            }
        }
        
        stage('Run Python Files') {
            steps {
                sh '''
                    python3 test.py
                    python3 h.py
                '''
            }
        }
    }
}
