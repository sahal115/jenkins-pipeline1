pipeline {
    agent any

    environment {
        AWS_REGION = 'us-west-2'
        IMAGE_ECR_REPO = '941377148643.dkr.ecr.us-west-2.amazonaws.com/jenkins-ci'
        ECR_REPO = '941377148643.dkr.ecr.us-west-2.amazonaws.com'
    }

    stages {

        stage('CodeScan') {
            steps {
                sh 'trivy fs . -o result.html'
            }
        }

        stage('dockerLogin') {
            steps {
                sh """
                    aws ecr get-login-password --region $AWS_REGION |
                    docker login --username AWS --password-stdin $ECR_REPO
                """
            }
        }

        stage('dockerImageBuild') {
            steps {
                sh 'docker build -t jenkins-ci:latest .'
                sh 'docker build -t imageversion:latest .'
            }
        }

        stage('dockerImageTag') {
            steps {
                // latest tag
                sh "docker tag jenkins-ci:latest $IMAGE_ECR_REPO:latest"

                // version tag
                sh "docker tag imageversion:latest $IMAGE_ECR_REPO:v1.$BUILD_NUMBER"
            }
        }

        stage('pushImage') {
            steps {
                sh "docker push $IMAGE_ECR_REPO:latest"
                sh "docker push $IMAGE_ECR_REPO:v1.$BUILD_NUMBER"
            }
        }
    }
}
