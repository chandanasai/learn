pipeline {
    agent any

    environment {
        // Define the S3 bucket name and the file to upload
        S3_BUCKET = 'learn-git-jenkins-s3'  // replace with your S3 bucket name
        FILE_TO_UPLOAD = 'profile.html'  // replace with the path to the file in your repo
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout from GitHub using the 'main' branch and stored credentials
                git branch: 'main', url: 'https://github.com/chandanasai/learn.git', credentialsId: 'ChandanaGit'
            }
        }

        stage('Upload to S3') {
            steps {
                // Use the AWS credentials stored in Jenkins credentials with ID 'ChandanaAWS'
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding', 
                    credentialsId: 'ChandanaAWS'
                ]]) {
                    // Use AWS CLI to upload the file to S3
                    bat """
                    aws s3 cp ${FILE_TO_UPLOAD} s3://${S3_BUCKET}/ --region us-east-1
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
