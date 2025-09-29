pipeline {
    agent any

    environment {
        COMPOSE_FILE = 'docker-compose.yaml'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Yashkumbhar1518/three-tier-mern-app.git'
            }
        }

        stage('Build & Deploy with Docker Compose') {
            steps {
                // Ensure we are in the repo root
                dir("${WORKSPACE}") {
                    echo "🛠️ Stopping old containers if any..."
                    sh 'docker-compose down -v || true'

                    echo "🚀 Building and starting containers..."
                    sh 'docker-compose up -d --build'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                echo "🔍 Checking backend status..."
                dir("${WORKSPACE}") {
                    sh 'docker ps'
                }
                echo "✅ Deployment should be live:"
                echo "Frontend: http://<EC2-PUBLIC-IP>:5173"
                echo "Backend: http://<EC2-PUBLIC-IP>:5050"
            }
        }
    }

    post {
        success {
            echo "🎉 MERN app deployed successfully on EC2!"
        }
        failure {
            echo "❌ Deployment failed. Check Jenkins console logs."
        }
    }
}
