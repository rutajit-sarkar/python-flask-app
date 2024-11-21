pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Setting up Python virtual environment and installing dependencies...'
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '''
                . venv/bin/activate
                python -m unittest discover -s .
                '''
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                mkdir -p /tmp/python-app-deploy
                cp app.py /tmp/python-app-deploy/
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for more details.'
        }
    }
}