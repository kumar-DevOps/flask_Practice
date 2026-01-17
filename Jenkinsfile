pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Setting up virtual environment and installing dependencies...'
                sh '''
                # Try to create venv
                python3 -m venv venv || { echo "Failed to create venv. Is python3-venv installed?"; exit 1; }

                # Check venv exists
                if [ ! -f "venv/bin/activate" ]; then
                    echo "venv/bin/activate not found. Install python3-venv on Jenkins agent."
                    exit 1
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
        }
        failure {
            echo "Build failed!"
        }
    }
}
