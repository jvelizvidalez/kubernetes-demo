pipeline {
  agent any
  stages {
    stage('Deploy') {
      agent {
      kubernetes {
          cloud 'kubernetes'
          defaultContainer 'jnlp'
        }
      }
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }
  }
  environment {
    imageName = 'jvelizvid/kubernetes-demo'
  }
}
