pipeline {
  agent any

  environment {
    AWS_DEFAULT_REGION = 'ap-south-1'
    BUCKET_NAME = 'my-static-webpage1111'
    AWS_ACCESS_KEY_ID = credentials('aws-access-key')
    AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
  }

  stages {
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
