pipeline {
    agent any

    tools {
        nodejs "nodejs"   // must match exactly the name in Jenkins → Tools
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/purushotham0912/my-react-app.git'
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
                sh '''
                  sudo rm -rf /var/www/html/my-react-app/*
                  sudo cp -r build/* /var/www/html/my-react-app/
                '''
            }
       
    }
}
