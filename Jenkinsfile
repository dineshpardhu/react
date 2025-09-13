pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key')   // Jenkins credentials
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'your-s3-bucket-name'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/react-s3-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync build/ s3://$S3_BUCKET --acl public-read --delete
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Website deployed to S3 successfully!'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
