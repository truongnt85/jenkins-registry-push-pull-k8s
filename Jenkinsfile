pipeline {

  environment {
    registry = "172.16.10.1:5000/frontend/myweb"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/truongnt85/jenkins-registry-push-pull-k8s.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          // sh '''sed -i "s/docker_tag/$BUILD_NUMBER/g"  myweb.yaml'''
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "Fintech-kubeconfig")
        }
      }
    }

  }

}
