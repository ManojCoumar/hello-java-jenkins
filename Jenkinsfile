pipeline {
    agent any

    environment {
        IMAGE = "hello-java-jenkins"
    }

    stages {

        stage('Build Maven') {
            steps {
                bat 'chmod +x mvnw'
                bat './mvnw clean package -DskipTests'                
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t $IMAGE:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s/'
                bat 'kubectl rollout status deployment/hello-java'
            }
        }
    }
}
