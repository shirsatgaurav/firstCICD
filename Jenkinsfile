pipeline {
    agent any

    environment {
        DEV_SERVER = "13.48.130.33"
        STG_SERVER = "51.20.138.15"
        PRD_SERVER = "13.60.242.151"
        WEB_DIR = "/var/www/html/"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to DEV') {
            when {
                branch 'Dev'
            }
            steps {
                echo "Deploying to DEV EC2"
                sh """
                scp index.html $DEV_SERVER:/tmp/
                ssh $DEV_SERVER 'sudo mv /tmp/index.html $WEB_DIR'
                """
            }
        }

        stage('Deploy to STAGING') {
            when {
                branch 'Stg'
            }
            steps {
                echo "Deploying to STG EC2"
                sh """
                scp index.html $STG_SERVER:/tmp/
                ssh $STG_SERVER 'sudo mv /tmp/index.html $WEB_DIR'
                """
            }
        }

        stage('Deploy to PRODUCTION') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying to PRD EC2"
                sh """
                scp index.html $PRD_SERVER:/tmp/
                ssh $PRD_SERVER 'sudo mv /tmp/index.html $WEB_DIR'
                """
            }
        }
    }
}
