pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Skipping dependency installation (pip not available on central server)'
            }
        }

        stage('Test') {
            steps {
                echo 'Skipping tests (would require dependencies)'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage completed'
            }
        }
    }
}
