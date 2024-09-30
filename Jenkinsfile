pipeline {
    agent any

    environment {
        // Define environment variables for AWS
        AWS_ACCESS_KEY_ID = credentials('ChandanaAWS')  // replace with your AWS access key credentials ID
        AWS_SECRET_ACCESS_KEY = credentials('ChandanaAWS')  // replace with your AWS secret key credentials ID
        S3_BUCKET = 'learn-git-jenkins-s3'  // replace with your S3 bucket name
        FILE_TO_UPLOAD = 'profile.html'  // replace with the path to the file in your repo
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout from GitHub using stored credentials
                git url: 'https://github.com/chandanasai/learn.git', credentialsId: 'ChandanaGit'
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    // Use AWS CLI to upload the file to S3 on a Windows machine
                    bat """
                    aws s3 cp ${FILE_TO_UPLOAD} s3://${S3_BUCKET}/
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'File uploaded successfully to S3!'
        }
        failure {
            echo 'File upload to S3 failed.'
        }
    }
}
