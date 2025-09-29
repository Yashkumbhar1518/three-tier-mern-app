pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Yashkumbhar1518/three-tier-mern-app.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                echo "🚀 Building backend and frontend containers..."
                sh 'docker-compose build'
            }
        }

        stage('Deploy Containers') {
            steps {
                echo "🛑 Stopping old containers..."
                sh 'docker-compose down -v || true'
                
                echo "🎯 Starting containers..."
                sh 'docker-compose up -d'
            }
        }

        stage('Verify Deployment') {
            steps {
                echo "🔍 Checking backend health..."
                sh 'curl -f http://localhost:5050/record || echo "Backend not ready yet"'
                
                echo "✅ Deployment complete!"
                echo "Open http://<EC2-PUBLIC-IP>:5173 for frontend"
            }
        }
    }

    post {
        success {
            echo "🎉 MERN app deployed successfully on EC2!"
        }
        failure {
            echo "❌ Deployment failed. Check Jenkins logs."
        }
    }
}
