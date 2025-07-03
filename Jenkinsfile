pipeline {
  agent any

  environment {
    AWS_DEFAULT_REGION = 'ap-south-1'  // Use your region
    BUCKET_NAME = 'my-static-webpage111'  // Your S3 bucket name
    AWS_ACCESS_KEY_ID = credentials('aws-access-key')
    AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
  }

  stages {
    stage('Clone Website Repo') {
      steps {
        git 'https://github.com/Sahana1110/Static-webpage.git'
      }
    }

    stage('Deploy to S3') {
      steps {
        sh '''
          aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
          aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
          aws configure set region $AWS_DEFAULT_REGION

          aws s3 sync . s3://$BUCKET_NAME --delete --exclude ".git/*"
        '''
      }
    }
  }
}
