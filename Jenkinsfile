pipeline {
    agent any

    environment {
        BRANCH_NAME = 'main'
        REPO_URL = 'https://github.com/purushotham0912/my-react-app.git'
        TARGET_HOST = 'ubuntu@52.66.207.95'
        TARGET_DIR = '/var/www/html/my-react-app'
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH_NAME}", url: "${REPO_URL}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    rm -rf node_modules package-lock.json
                    npm install
                '''
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh """
                    ssh -o StrictHostKeyChecking=no ${TARGET_HOST} "sudo rm -rf ${TARGET_DIR}/*"
                    scp -o StrictHostKeyChecking=no -r build/* ${TARGET_HOST}:${TARGET_DIR}/
                """
            }
        }

        stage('Reload Nginx') {
            steps {
                sh "ssh -o StrictHostKeyChecking=no ${TARGET_HOST} 'sudo systemctl reload nginx'"
            }
        }
    }

    post {
        failure {
            echo '❌ Pipeline failed!'
        }
        success {
            echo '✅ Pipeline completed successfully!'
        }
    }
}
