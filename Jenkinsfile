pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/purushotham0912/my-react-app.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                sudo rm -rf /var/www/html/my-react-app/*
                sudo cp -r build/* /var/www/html/my-react-apppp/
                '''
            }
        }
    }
}
