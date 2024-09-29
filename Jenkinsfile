pipeline {
    agent any

    environment {
        // Use the IDs of the stored AWS credentials
        AWS_ACCESS_KEY_ID = credentials('ChandanaAWS')
        AWS_SECRET_ACCESS_KEY = credentials('ChandanaAWS') 
        S3_BUCKET = 'learn-git-jenkins-s3' 
        FILE_TO_UPLOAD = 'profile.html'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    // Upload the file to S3
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
