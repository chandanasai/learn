pipeline {
    agent any

    environment {
        // Define environment variables for AWS
        AWS_ACCESS_KEY_ID = credentials('AKIA3FLD4MPNWIFUZ6MS') 
        AWS_SECRET_ACCESS_KEY = credentials('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') 
        S3_BUCKET = 'learn-git-jenkins-s3'  
        FILE_TO_UPLOAD = 'profile-hw2.html' 
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
                    // Use AWS CLI to upload the file to S3
                    sh """
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
