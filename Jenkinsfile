pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                withKubeConfig([credentialsId: 'mykubeconfig', serverUrl: '']) {
                    sh 'kubectl get namespaces'
                }
            }
        }
    }
}
