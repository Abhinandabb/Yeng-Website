pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy to Azure Storage') {
            steps {
                sh '''
                az storage blob upload-batch \
                  --account-name <basic12> \
                  --destination '$web' \
                  --source .
                '''
            }
        }
    }
}
