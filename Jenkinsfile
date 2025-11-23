pipeline {
    agent any

    environment {
        // Jenkins credentials ID for Gmail (Username with App Password)
        EMAIL_CREDENTIALS = '7df8a63a-e7bb-40d7-bb0e-0ed05e4766a4'
        RECIPIENT = 'deeps19nija@gmail.com'
        VENV_DIR = 'venv'
        FLASK_LOG = 'nohup.out'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Setting up virtual environment and installing dependencies...'
                sh '''
                # Remove old virtual environment if exists
                rm -rf ${VENV_DIR}
                # Create virtual environment
                python3 -m venv ${VENV_DIR}
                # Activate venv
                . ${VENV_DIR}/bin/activate
                # Upgrade pip
                pip install --upgrade pip
                # Install dependencies
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests with pytest...'
                sh '''
                . ${VENV_DIR}/bin/activate
                # Install pytest if not already installed
                pip install pytest
                # Run tests
                pytest
                '''
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying Flask app to staging...'
                sh '''
                . ${VENV_DIR}/bin/activate
                # Run Flask app in background using nohup
                nohup python3 app.py > ${FLASK_LOG} 2>&1 &
                echo "Flask app deployed and running in background. Logs: ${FLASK_LOG}"
                '''
            }
        }
    }

    post {
        success {
            echo 'Build succeeded, sending success email...'
            emailext (
                to: "${RECIPIENT}",
                subject: "Jenkins Build Success: ${JOB_NAME} #${BUILD_NUMBER}",
                body: "The Jenkins pipeline completed successfully.\n\nCheck logs at ${BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                from: "${RECIPIENT}",
                replyTo: "${RECIPIENT}"
            )
        }

        failure {
            echo 'Build failed, sending failure email...'
            emailext (
                to: "${RECIPIENT}",
                subject: "Jenkins Build Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                body: "The Jenkins pipeline failed. Check the console output:\n${BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                from: "${RECIPIENT}",
                replyTo: "${RECIPIENT}"
            )
        }
    }
}
