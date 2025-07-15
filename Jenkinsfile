pipeline {
    agent any

    environment {
        K8S_TOKEN_ID = 'k8-token'
        CLUSTER_NAME = 'EKS-1'
        NAMESPACE = 'webapps'
        K8S_API_URL = 'https://883C2C11426CD902578376CB7DBC9B11.yl4.ap-south-1.eks.amazonaws.com'
    }

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    credentialsId: "${K8S_TOKEN_ID}",
                    clusterName: "${CLUSTER_NAME}",
                    contextName: '',
                    namespace: "${NAMESPACE}",
                    serverUrl: "${K8S_API_URL}",
                    caCertificate: ''
                ]]) {
                    sh 'kubectl apply -f deployment-service.yml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    credentialsId: "${K8S_TOKEN_ID}",
                    clusterName: "${CLUSTER_NAME}",
                    contextName: '',
                    namespace: "${NAMESPACE}",
                    serverUrl: "${K8S_API_URL}",
                    caCertificate: ''
                ]]) {
                    sh 'kubectl get all -n ${NAMESPACE}'
                }
            }
        }
    }
}
