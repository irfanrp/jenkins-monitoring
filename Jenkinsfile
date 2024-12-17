pipeline {
    agent any
    environment {s
        KUBERNETES_NAMESPACE = 'monitoring'  // Replace with your namespace
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout your repository
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'git@github.com:irfanrp/jenkins-integration.git']])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh '''
                        docker build -t $DOCKER_IMAGE .
                    '''
                }
            }
        }
        stage('Deploy again to Kubernetes') {
            steps {
                script {
                    // Deploy to Kubernetes using kubectl
                    sh '''
                        kubectl apply -f k8s/deployment.yaml -n $KUBERNETES_NAMESPACE
                    '''
                }
            }
        }
        stage('rollout restart  Kubernetes') {
            steps {
                script {
                    // Deploy to Kubernetes using kubectl
                    sh '''
                        kubectl rollout restart deployment/helloworld-app -n $KUBERNETES_NAMESPACE
                    '''
                }
            }
        }
    }
    post {
        always {
            // Clean up if necessary, for example, remove the Docker image locally
            sh 'docker rmi $DOCKER_IMAGE'
        }
    }
}
