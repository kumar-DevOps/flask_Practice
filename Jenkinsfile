pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Setting up virtual environment and installing dependencies...'
                sh '''
                # Create virtual environment if not exists
                if [ ! -d "venv" ]; then
                    python3 -m venv venv
                fi

                # Activate venv
                . venv/bin/activate

                # Upgrade pip inside venv
                pip install --upgrade pip setuptools wheel

                # Install project dependencies
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh '''
                . venv/bin/activate
                pytest tests/ --maxfail=1 --disable-warnings -q
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Flask app to staging...'
                sh '''
                . venv/bin/activate
                pkill -f gunicorn || true
                nohup gunicorn -w 4 -b 0.0.0.0:8000 app:app &
                '''
            }
        }
    }

    post {
        success {
            echo "Build succeeded!"
            // Uncomment mail step once SMTP is configured
            // mail to: 'team@example.com',
            //      subject: "SUCCESS: Jenkins Build #${BUILD_NUMBER}",
            //      body: "The build succeeded! Check Jenkins for details."
        }
        failure {
            echo "Build failed!"
            // Uncomment mail step once SMTP is configured
            // mail to: 'team@example.com',
            //      subject: "FAILED: Jenkins Build #${BUILD_NUMBER}",
            //      body: "The build failed. Please check Jenkins logs."
        }
    }
}
