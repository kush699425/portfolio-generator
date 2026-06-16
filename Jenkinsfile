pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio-generator:v1 .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop portfolio-app || true
                docker rm portfolio-app || true
                docker run -d --name portfolio-app -p 5000:5000 portfolio-generator:v1
                '''
            }
        }
    }
}
