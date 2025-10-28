pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KowshikT/Jen.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t ci-demo-nginx .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run --rm ci-demo-nginx nginx -t'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                docker stop ci-demo-container || true
                docker rm ci-demo-container || true
                docker run -d --name ci-demo-container -p 8082:80 ci-demo-nginx
                '''
            }
        }
    }
}
