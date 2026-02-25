pipeline {
    agent any

    environment {
        IMAGE = "hello-java-jenkins"
    }

    stages {

        stage('Build Maven') {
            steps {
                bat 'mvn clean package -DskipTests'                
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t hello-java-jenkins:latest .'
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
