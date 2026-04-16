pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        DOCKERHUB_USER = "pavankandula"   // CHANGE THIS
        CONTAINER_NAME = "myapp-container"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }

        stage('Test Container') {
            steps {
                sh 'sleep 5'
                sh 'curl -f http://localhost:3000 || exit 1'
            }
        }

     stage('Push Image to DockerHub') {
    steps {
        script {
            withDockerRegistry([credentialsId: 'dockerhub-creds']) {
             sh 'docker tag myapp pavankandula/myapp:latest'
             sh 'docker push pavankandula/myapp:latest'
            }
        }
    }
}
    }

    post {
        always {
            sh 'docker images | grep myapp || true'
        }
    }
}
