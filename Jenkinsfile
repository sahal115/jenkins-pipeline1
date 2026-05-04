pipeline {
    agent any

    stages {
        stage('CodeScan') {
            steps {
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
            }
        }
        stage('dockerLogin'){
            steps{
                sh 'aws ecr get-login-password --region us-west-2 | \
                 docker login --username AWS \
                  --password-stdin 941377148643.dkr.ecr.us-west-2.amazonaws.com'
            }
        }


        stage('dockerImageBuild') { 
            steps {
                sh 'docker build -t jenkins-ci .'
            }
        }
        stage('dockerImageTag'){
            steps{
                sh 'docker tag jenkins-ci:latest \
                 941377148643.dkr.ecr.us-west-2.amazonaws.com/jenkins-ci:latest'
            }
        }
            

        stage('pushImage') {
            steps {
                sh 'docker push \
                 941377148643.dkr.ecr.us-west-2.amazonaws.com/jenkins-ci:latest'
            }
        }
    }
}