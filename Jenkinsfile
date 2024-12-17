pipeline {
    agent any
    environment {
        KUBERNETES_NAMESPACE = 'monitoring'  // Replace with your namespace
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'git@github.com:irfanrp/jenkins-monitoring.git']])
            }
        }
    
        stage('Deploy again to Kubernetes') {
            steps {
                script {
                    // Deploy to Kubernetes using kubectl
                    sh '''
                        kubectl apply -f grafana.yaml -n $KUBERNETES_NAMESPACE
                    '''
                }
            }
        }
    }
}
