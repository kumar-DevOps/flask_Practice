pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'pytest tests/ --maxfail=1 --disable-warnings -q'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Flask app to staging...'
                sh '''
                pkill -f gunicorn || true
                nohup gunicorn -w 4 -b 0.0.0.0:8000 app:app &
                '''
            }
        }
    }

    post {
        success {
            mail to: 'team@example.com',
                 subject: "SUCCESS: Jenkins Build #${BUILD_NUMBER}",
                 body: "The build succeeded! Check Jenkins for details."
        }
        failure {
            mail to: 'team@example.com',
                 subject: "FAILED: Jenkins Build #${BUILD_NUMBER}",
                 body: "The build failed. Please check Jenkins logs."
        }
    }
}
