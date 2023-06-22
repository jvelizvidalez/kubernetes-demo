pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'node'
        }

      }
      environment {
        imageName = 'jvelizvid/kubernetes-demo'
      }
      steps {
        nodejs 'NodeJS'
        sh 'yarn install'
        sh 'yarn run build'
        sh 'tar -cvf builtSources.tar ./dist/'
        stash(name: 'dist-files', includes: 'builtSources.tar', useDefaultExcludes: true)
      }
    }

  }
}