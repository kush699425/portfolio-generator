pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t portfolio-generator:v1 .'
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag portfolio-generator:v1 kush699425/portfolio-generator:v1'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push kush699425/portfolio-generator:v1'
            }
        }

        stage('Production Server') {
            steps {
                sh '''
                ssh ec2-user@13.233.105.33 "
                podman pull docker.io/kush699425/portfolio-generator:v1
                podman stop portfolio-app || true
                podman rm portfolio-app || true
                podman run -d --name portfolio-app -p 5000:5000 docker.io/kush699425/portfolio-generator:v1
                "
                '''
            }
        }
    }
}
