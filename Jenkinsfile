pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                sh 'trivy --version'
                
                
            }
        }

        stage('test ') {
            steps {
                sh 'docker --v'
            }
        }

        stage('pushImage') {
            steps {
                sh 'docker ps'
            }
        }
    }
}