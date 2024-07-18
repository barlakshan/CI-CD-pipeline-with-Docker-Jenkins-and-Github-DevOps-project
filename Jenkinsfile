pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/barlakshan/CI-CD-pipeline-with-Docker-Jenkins-and-Github-DevOps-project.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t barlakshan/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-password', variable: 'dockerhubPass')]) {
                    script {
                        bat "docker login -u barlakshan -p %dockerhubPass%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push barlakshan/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
        
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
