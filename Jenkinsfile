pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {pipeline {
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

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker ps -q --filter "name=gaming-app" | grep -q . && docker stop gaming-app || true
                docker ps -aq --filter "name=gaming-app" | grep -q . && docker rm gaming-app|| true
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

        stage('Verify Container') {
            steps {
                sh 'docker ps | grep gaming-app'
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
                sh 'docker build -t gaming-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop gaming || true'
                sh 'docker rm gaming || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name gaming gaming-app'
            }
        }

        stage('Deploy Frontend') {
            steps {
                sh 'sudo cp -r frontend/* /usr/share/nginx/html/'
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}
