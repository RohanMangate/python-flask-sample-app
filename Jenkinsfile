pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies'
                sh 'python3 -m pip install --upgrade pip'
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                sh 'pytest || true'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Flask application'
                sh 'nohup python3 app.py &'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
