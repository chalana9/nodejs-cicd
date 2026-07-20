pipeline {

    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test Application') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodejs-cicd-app:v1 .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop node-app || true
                docker rm node-app || true
                docker run -d \
                -p 3000:3000 \
                --name node-app \
                nodejs-cicd-app:v1
                '''
            }
        }
    }
}
