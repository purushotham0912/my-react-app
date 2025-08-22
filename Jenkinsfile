pipeline {
    agent any
 
    environment {
        NODE_ENV = 'production'
    }
 
    stages {
        stage('Clone Repository') {
            steps {
                git url: https://github.com/purushotham0912/my-react-app.git
            }
        }
 
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
 
        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }
 
        stage('List Build Output') {
            steps {
                sh 'ls -l build'
            }
        }
    }
 
    post {
        success {
            echo "✅ React app built successfully!"
        }
        failure {
            echo "❌ Build failed. Check logs above."
        }
    }
}
