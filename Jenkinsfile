pipeline {
  agent any
  stages {
    stage('') {
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

  }
}