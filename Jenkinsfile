pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies'
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
                echo 'Running unit tests'
                sh '''
                    . venv/bin/activate
                    pytest test_app.py -v
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application to staging'
                sh '''
                    . venv/bin/activate
                    nohup python3 app.py &
                    sleep 3
                    echo "Application deployed successfully on port 5000"
                '''
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
    }
}
