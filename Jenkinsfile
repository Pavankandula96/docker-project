pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        DOCKERHUB_USER = "pavankandula"
        CONTAINER_NAME = "myapp-container"
        EC2_IP = 3.84.245.38
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
                sh 'curl -f http://localhost:3000'
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                    docker tag $IMAGE_NAME $DOCKER_USER/$IMAGE_NAME:latest
                    docker push $DOCKER_USER/$IMAGE_NAME:latest
                    '''
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ec2-user@$EC2_IP "
                docker rm -f myapp-container || true
                docker pull $DOCKERHUB_USER/$IMAGE_NAME:latest
                docker run -d -p 3000:80 --name myapp-container $DOCKERHUB_USER/$IMAGE_NAME:latest
                "
                '''
            }
        }
    }

    post {
        always {
            sh 'docker images | grep myapp || true'
        }
    }
}
