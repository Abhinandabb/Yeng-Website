pipeline {
    agent any

    environment {
        IMAGE_NAME = "yeng-website:latest"
        KUBECONFIG = "/root/.kube/config"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Abhinandabb/Yeng-Website'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Optional: Use Minikube Docker if you want images directly there
                sh 'eval $(minikube -p minikube docker-env) || true'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy to Minikube') {
            steps {
                sh 'kubectl get nodes'
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f services.yaml'
            }
        }
    }

    post {
        success {
            echo "Deployment successful ✅"
        }
        failure {
            echo "Deployment failed ❌"
        }
    }
}
