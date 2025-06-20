pipeline {
    agent any
    environment {
        MINIKUBE_HOME = "/home/icha"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t company-profile:latest .'
            }
        }

        stage('Load to Minikube') {
            steps {
                sh 'minikube image load company-profile:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                    kubectl apply -f k8s/ingress.yaml
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment berhasil!'
        }
        failure {
            echo '❌ Deployment gagal!'
        }
        always {
            echo '📦 Pipeline selesai dijalankan.'
        }
    }
}
