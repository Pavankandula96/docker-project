pipeline {
    agent any

 

    environment {
        SCANNER_HOME = tool 'mysonar'
    }

    stages {

        stage('Clean') {
            steps { cleanWs() }
        }

        stage('Checkout Code') {
            steps {
                git 'https://github.com/YOUR_USERNAME/docker-devops-project.git'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('mysonar') {
                    sh """
                    $SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.projectKey=devops-project \
                    -Dsonar.projectName=devops-project
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('OWASP Scan') {
            steps {
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'DP-Check'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy fs . > trivy.txt'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }

        stage('Push Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-password') {
                        sh 'docker tag myapp YOUR_DOCKERHUB/myapp:latest'
                        sh 'docker push YOUR_DOCKERHUB/myapp:latest'
                    }
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 3000:3000 YOUR_DOCKERHUB/myapp:latest'
            }
        }
    }
}
