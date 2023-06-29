pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        dockerfile {
          filename 'Dockerfile'
        }
      }
      steps {
        echo 'Build stage'
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
  }
  environment {
    imageName = 'jvelizvid/kubernetes-demo'
  }
}
