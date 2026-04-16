pipeline {
    agent any

    stages {

        stage('Clean') {
            steps { cleanWs() }
        }

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Pavankandula96/docker-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name myapp-container myapp || true'
            }
        }
    }
}
