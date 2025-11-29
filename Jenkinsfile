pipeline {
    agent any

    stages {
        stage('Environment Setup') {
            steps {
                echo 'Setting up environment...'
                // Checkout code
                checkout scm
                // Install dependencies
                sh 'python3 -m venv venv'
                sh 'source venv/bin/activate && pip install --upgrade pip'
                sh 'source venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Pipeline Compilation') {
            steps {
                echo 'Compiling Kubeflow pipeline...'
                sh 'source venv/bin/activate && python3 pipeline.py'
            }
        }

        stage('Completion') {
            steps {
                echo 'All stages completed successfully!'
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline finished successfully!'
        }
        failure {
            echo 'CI Pipeline failed.'
        }
    }
}

