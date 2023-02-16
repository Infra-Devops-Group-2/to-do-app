pipeline {
    agent any
    environment {
            DOCKER_IMAGE = credentials('ecr-docker-image-id')
            ECR_REGISTRY = credentials('ecr-registry')
       }
    stages {
        stage ('Build') {
            steps {
                sh "aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin $ECR_REGISTRY"
                sh "docker build -t $ECR_REGISTRY/$DOCKER_IMAGE ."
            }
        }
        stage ('Push to registry') {
            steps {
                sh "docker push $ECR_REGISTRY/$DOCKER_IMAGE"
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