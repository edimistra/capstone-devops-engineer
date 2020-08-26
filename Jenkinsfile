pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './support_scripts/run_docker.sh'
      }
    }
    stage('Push Docker Image to AWS ECR') {
      steps {
        sh 'aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 678583983523.dkr.ecr.us-west-2.amazonaws.com'
        sh 'docker tag nginx-hello:latest 678583983523.dkr.ecr.us-west-2.amazonaws.com/nginx-hello:latest'
        sh 'docker push 678583983523.dkr.ecr.us-west-2.amazonaws.com/nginx-hello:latest'
      }
    }
  }
}
