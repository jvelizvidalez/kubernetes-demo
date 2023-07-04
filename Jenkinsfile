stage ('Deploy to Cluster') {
    steps {
        //withAWS(role: "Jenkins", roleAccount: '164135465533') {
        sh "aws eks update-kubeconfig --region eu-west-2 --name ekscluster"
       // sh "aws eks update-kubeconfig --region eu-west-1 --name switch-arca-qa-cluster"
        sh " envsubst < ${WORKSPACE}/deploy.yaml | ./kubectl apply -f - "
        //}
    }
}
