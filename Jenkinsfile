// pipeline {
//     agent any
//     stages {
//         stage('Checkout') {
//             steps { git 'https://github.com/Abhinandabb/Yeng-Website.git' }
//         }
//         stage('Build Image') {
//             steps { sh 'docker build -t yeng-website:latest .' }
//         }
//         stage('Load Image into Minikube') {
//             steps { sh 'minikube image load yeng-website:latest' }
//         }
//         stage('Deploy') {
//             steps {
//                 sh '''
//                 kubectl apply -f deployment.yaml
//                 kubectl apply -f services.yaml
//                 kubectl rollout status deployment/yeng-website
//                 '''
//             }
//         }
//     }
// }


pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Abhinandabb/Yeng-Website.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t yeng-website:latest .'
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                    docker tag yeng-website:latest abhinandabb/yeng-website:latest
                    docker push abhinandabb/yeng-website:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    kubectl apply -f deployment.yaml
                    kubectl rollout status deployment/yeng-website
                '''
            }
        }
    }
}

