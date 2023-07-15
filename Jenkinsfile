pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        script {
            def customImage = docker.build imageName
        }
      }
    }
    stage('Publish') {
      environment {
        registryCredential = 'dockerhub-credentials'
      }
      steps {
        script {
          def appimage = docker.build imageName
          docker.withRegistry( '', registryCredential ) {
            appimage.push()
            if (env.BRANCH_NAME == 'main' || env.BRANCH_NAME == 'release') {
              appimage.push('latest')
              if (env.BRANCH_NAME == 'release') {
                appimage.push("release-" + "${COMMIT_SHA}")
              }
            }
          }
        }
      }
    }
    stage('Deploy') {
      steps {
        withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: '']) {
            pwsh 'kubectl apply -f deployment.yaml'
            pwsh 'kubectl apply -f service.yaml'
        }
      }
    }
  }
  environment {
    imageName = 'jvelizvid/kubernetes-demo'
  }
}
