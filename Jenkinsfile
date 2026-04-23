pipeline {
    agent any

    environment {
        APP_NAME = "gaming"
        IMAGE_NAME = "gaming-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Gurraiah123/gaming-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t gaming-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop gaming || true
                docker rm gaming || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 5000:5000 --name gaming gaming-app
                '''
            }
        }

        stage('Deploy Frontend') {
            steps {
                sh '''
                sudo rm -rf /usr/share/nginx/html/*
                sudo cp -r frontend/* /usr/share/nginx/html/
                sudo systemctl restart nginx
                '''
            }
        }
    }
}
