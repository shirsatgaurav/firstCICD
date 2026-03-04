pipeline {
    agent any

    environment {
        APP_DIR = "/var/www/html"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning application code from GitHub..."
                git branch: 'main',
                    url: 'https://github.com/shirsatgaurav/firstCICD.git'
            }
        }

        stage('Install Apache') {
            steps {
                echo "Installing Apache HTTPD..."
                sh '''
                sudo yum install -y httpd
                '''
            }
        }

        stage('Start Apache Service') {
            steps {
                echo "Starting Apache service..."
                sh '''
                sudo systemctl start httpd
                sudo systemctl enable httpd
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                echo "Deploying static application..."
                sh '''
                sudo rm -rf ${APP_DIR}/*
                sudo cp -r . ${APP_DIR}/
                sudo chown -R apache:apache ${APP_DIR}
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                echo "Verifying Apache service..."
                sh '''
                sudo systemctl is-active httpd
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Application is live."
        }
        failure {
            echo "❌ Deployment failed. Please check logs."
        }
    }
}
