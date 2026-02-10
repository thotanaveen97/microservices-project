pipeline {
    agent any

    environment {
        K8S_TOKEN = credentials('k8-token')
    }

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(
                    kubeconfigContent: """
apiVersion: v1
kind: Config
clusters:
- name: EKS-1
  cluster:
    server: https://B27A35796AEBCA5752F7DA4E7485C201.gr7.us-east-1.eks.amazonaws.com
contexts:
- name: jenkins
  context:
    cluster: EKS-1
    user: jenkins
    namespace: webapps
current-context: jenkins
users:
- name: jenkins
  user:
    token: ${K8S_TOKEN}
"""
                ) {
                    sh 'kubectl apply -f deployment-service.yml'
                }
            }
        }

        stage('verify Deployment') {
            steps {
                sh 'kubectl get svc -n webapps'
            }
        }
    }
}
