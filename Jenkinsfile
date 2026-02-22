pipeline {
    agent any
    
    environment {
        PYTHON_VERSION = '3.9'
        PROJECT_NAME = 'OCC'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Setup Python Environment') {
            steps {
                echo 'Setting up Python environment...'
                sh '''
                    python3 --version
                    pip3 --version
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh '''
                    if [ -f requirements.txt ]; then
                        pip3 install -r requirements.txt
                    else
                        echo "No requirements.txt found, skipping..."
                    fi
                '''
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh '''
                    python3 test.py
                    python3 h.py
                '''
            }
        }
        
        stage('Code Quality Check') {
            steps {
                echo 'Running code quality checks...'
                sh '''
                    if command -v pylint &> /dev/null; then
                        pylint *.py || echo "Pylint checks completed with warnings"
                    else
                        echo "Pylint not installed, skipping..."
                    fi
                '''
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                echo 'Archiving artifacts...'
                archiveArtifacts artifacts: '*.py, README.md', allowEmptyArchive: true
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
