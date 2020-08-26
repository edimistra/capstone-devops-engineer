pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh 'docker build -t nginx-hello .'
      }
    }
    stage('Push Docker Image to AWS ECR') {
      steps {
        withDockerRegistry([url: "678583983523.dkr.ecr.us-west-2.amazonaws.com/nginx-hello", credentialsId: "ecr:us-west-2:jenkins"]) {
        sh 'docker push 678583983523.dkr.ecr.us-west-2.amazonaws.com/nginx-hello:latest'
        }
      }
    }
  }
}