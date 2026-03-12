pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven'
    }    
    environment {
        IMAGE = "hello-java-jenkins"
        KUBECONFIG = "kubeconfig-ci.yml"
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

        stage('Load Image to Minikube') {
            steps {
                bat 'minikube image load hello-java-jenkins:latest'
            }
        }    
        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl --kubeconfig=kubeconfig-ci.yml apply -f k8s/'
                bat 'kubectl --kubeconfig=kubeconfig-ci.yml rollout status deployment/hello-java'
                bat 'kubectl --kubeconfig=kubeconfig-ci.yml get pods'
                bat 'kubectl --kubeconfig=kubeconfig-ci.yml get services'
            }
        }
    }
}
