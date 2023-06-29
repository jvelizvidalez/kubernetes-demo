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
        nodejs('NodeJS') {
          sh 'yarn install --frozen-lockfile'
        }
      }
    }
    stage('Publish') {
      environment {
        registryCredential = 'dockerhub-credentials'
      }
      steps {
        unstash 'dist-files'
        sh 'tar -xvf builtSources.tar'
        script {
          commitId = sh(returnStdout: true, script: 'git rev-parse --short HEAD')
          def appimage = docker.build imageName + ":" + commitId.trim()
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
    imageName = 'kubernetes-demo'
  }
}
