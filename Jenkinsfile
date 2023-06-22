pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'node:14-buster'
        }
      }
      steps {
        sh 'yarn install --frozen-lockfile'
        sh 'yarn run build'
        sh 'tar -cvf builtSources.tar ./dist/'
        stash(name: 'dist-files', includes: 'builtSources.tar', useDefaultExcludes: true)
      }
    }
  }
  environment {
    imageName = 'example-service'
  }
}