pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }

        stage('Deploy to Staging') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                sh '''
                . venv/bin/activate
                nohup python app.py > flask.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            emailext(
                to: "your-email@example.com",
                subject: "Jenkins Build Successful",
                body: "The Jenkins pipeline executed successfully."
            )
        }
        failure {
            emailext(
                to: "your-email@example.com",
                subject: "Jenkins Build Failed",
                body: "The Jenkins pipeline failed."
            )
        }
    }
}
