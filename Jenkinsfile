pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        docker.build('nginx-hello')
      }
    }
    stage('Push Docker Image to AWS ECR') {
      steps {
        docker.withRegistry('678583983523.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:aws-static') {
          docker.image('nginx-hello').push('latest')
        }
      }
    }
  }
}