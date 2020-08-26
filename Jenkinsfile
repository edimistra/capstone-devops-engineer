pipeline {
  agent any
  stages {
    stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./nginx-hello/*.html'
			}
		}
    stage('Docker Build') {
      steps {
        sh 'docker build -t nginx-hello .'
      }
    }
    stage('Push Docker Image to AWS ECR') {
      steps {
        withDockerRegistry([url: 'https://678583983523.dkr.ecr.us-west-2.amazonaws.com', credentialsId: 'ecr:us-west-2:jenkins']) {
        sh '''
          docker tag nginx-hello:latest 678583983523.dkr.ecr.us-west-2.amazonaws.com/nginx-hello:latest
          docker push 678583983523.dkr.ecr.us-west-2.amazonaws.com/nginx-hello:latest
        '''
        }
      }
    }
    stage('Create the cluster configuration file') {
			steps {
				withAWS(region:'us-west-2', credentials:'jenkins') {
					sh 'aws eks --region us-west-2 update-kubeconfig --name capstoneCluster'
				}
			}
		}
    stage('Set current kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'jenkins') {
					sh 'kubectl config use-context arn:aws:eks:us-west-2:678583983523:cluster/capstoneCluster'
				}
			}
		}
  }
}