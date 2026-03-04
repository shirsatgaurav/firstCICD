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
                url: https://github.com/shirsatgaurav/firstCICD.git
            }
        }

        stage('Install Apache') {
            steps {
                echo "Installing Apache HTTPD..."
                sh '''
                sudo yum update -y
                sudo yum install httpd -y
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
                sudo rm -rf /var/www/html/*
                sudo cp -r * /var/www/html/
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                echo "Checking Apache status..."
                sh '''
                systemctl status httpd
                '''
            }
        }
    }
}
