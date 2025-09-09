pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html/my-react-app"
    }

    stages {
        stage('Checkout') {
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
        sh '''
            # Clean old build folder (fix permission issues)
            sudo rm -rf build

            # Build fresh
            npm run build
        '''
    }
}


        stage('Deploy') {
            steps {
                sh '''
                    # Ensure deploy directory exists
                    sudo mkdir -p $DEPLOY_DIR

                    # Clean old files
                    sudo rm -rf $DEPLOY_DIR/*

                    # Copy new build
                    sudo cp -r build/* $DEPLOY_DIR/

                    # Reload nginx to serve updated files
                    sudo systemctl reload nginx
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! React app is live."
        }
        failure {
            echo "❌ Deployment failed. Check Jenkins logs."
        }
    }
}
