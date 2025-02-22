pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'rohan759/simple-app:latest'  // Using your Docker Hub username
        KUBECONFIG = '/var/lib/jenkins/kubeconfig/kubeconfig.yaml'  // Path to your kubeconfig file on the Jenkins server
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/rohanshinge7/Devops-CapStone.git'  // Using your GitHub username
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package -DskipTests'  // Skipping tests if unnecessary
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'  // Ensure that your deployment YAML file is in the repository
            }
        }
    }
}

