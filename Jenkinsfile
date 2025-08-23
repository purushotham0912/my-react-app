pipeline {
    agent any

    tools {
        nodejs "nodejs"   // or "NodeJS-20" if you configured it in Jenkins
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/purushotham0912/my-react-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'sudo cp -r build/* /var/www/html/my-react-app/'
            }
        }
    }
}
