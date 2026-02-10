pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(
                    kubectlCredentials: [[
                        credentialsId: 'k8-token',
                        serverUrl: 'https://B27A35796AEBCA5752F7DA4E7485C201.gr7.us-east-1.eks.amazonaws.com',
                        clusterName: 'EKS-1',
                        namespace: 'webapps'
                    ]]
                ) {
                    sh 'kubectl apply -f deployment-service.yml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(
                    kubectlCredentials: [[
                        credentialsId: 'k8-token',
                        serverUrl: 'https://B27A35796AEBCA5752F7DA4E7485C201.gr7.us-east-1.eks.amazonaws.com',
                        clusterName: 'EKS-1',
                        namespace: 'webapps'
                    ]]
                ) {
                    sh 'kubectl get svc'
                }
            }
        }
    }
}
