pipeline {
    agent any

    stages {

        stage('Clean') {
            steps { cleanWs() }
        }

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Run Container') {
            steps {
               sh 'docker run -d -p 3000:80 --name myapp-container myapp || true'
            }
        }
    }
}
