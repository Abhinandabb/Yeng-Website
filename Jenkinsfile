pipeline {
    agent any

    environment {
        IMAGE_NAME = "yeng-website:latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                
                git 'https://github.com/Abhinandabb/Yeng-Website'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $yeng-website:latest .'
            }
        }

        stage('Deploy to Minikube') {
            steps {
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
