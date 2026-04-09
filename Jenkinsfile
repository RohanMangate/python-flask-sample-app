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
            mail to: 'rvmangate@gmail.com',
                 subject: "SUCCESS: Jenkins Build - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The pipeline ${env.JOB_NAME} build #${env.BUILD_NUMBER} completed successfully.\n\nCheck: ${env.BUILD_URL}"
        }
        failure {
            echo 'Pipeline failed!'
            mail to: 'rvmangate@gmail.com',
                 subject: "FAILURE: Jenkins Build - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The pipeline ${env.JOB_NAME} build #${env.BUILD_NUMBER} failed.\n\nCheck: ${env.BUILD_URL}"
        }
    }
}
