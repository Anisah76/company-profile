pipeline {
    agent any
    environment {
        MINIKUBE_HOME = "/home/anisa"
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
            // Kalau mau kirim notifikasi ke Discord/Email bisa ditambahkan di sini
        }
        failure {
            echo '❌ Deployment gagal!'
            // Bisa juga ditambahkan notifikasi kegagalan
        }
        always {
            echo '📦 Pipeline selesai dijalankan.'
            // Biasanya untuk cleanup workspace atau hapus file temporary
            // cleanWs() // uncomment kalau mau otomatis hapus workspace
        }
    }
}
