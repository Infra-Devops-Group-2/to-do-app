pipeline {
    agent any
    stages {
        stage ('Build') {
            steps {
                sh "aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 154647635698.dkr.ecr.ap-southeast-1.amazonaws.com"
                sh "docker build -t 154647635698.dkr.ecr.ap-southeast-1.amazonaws.com/argonauts:latest ."
            }
        }
        stage ('Push to registry') {
            steps {
                sh "docker push 154647635698.dkr.ecr.ap-southeast-1.amazonaws.com/argonauts:latest"
            }
        }
        stage ('Deploy') {
            steps {
                sh "kubectl apply -f deployments/deployment.yaml"
                sh "kubectl apply -f deployments/service.yaml"
            }
        }
    }
}