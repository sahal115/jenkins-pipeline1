pipeline {
    agent any

    stages {
        stage('CodeScan') {
            steps {
                sh '''
            export PATH=$PATH:/usr/local/bin
            trivy --version
        '''
            }
        }

        stage('dockerImageBuild') {
            steps {
                sh 'docker -v'
            }
        }

        stage('pushImage') {
            steps {
                sh 'docker ps'
            }
        }
    }
}