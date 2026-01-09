pipeline {
    agent any

    environment {
        K8S_TOKEN_ID = 'k8-token'
        CLUSTER_NAME = 'EKS-1'
        NAMESPACE = 'webapps'
        K8S_API_URL = 'https://A824161849B6E54D63A379C0C36E3D79.gr7.ap-south-1.eks.amazonaws.com'
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
                    sh '''
                        kubectl get pods -n ${NAMESPACE}
                        kubectl get svc -n ${NAMESPACE}
                        kubectl get deploy -n ${NAMESPACE}
                    '''
                }
            }
        }
    }
}
