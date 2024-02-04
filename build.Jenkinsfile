pipeline {
    agent any

    environment {
        IMAGE_NAME = 'orrmb/roberta'
        IMAGE_TAG  = '0.0.$BUILD_NUMBER'
    }

    stages {
        stage('Docker Hub login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker_Hub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "docker login -u $USER -p $PASS"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t "${IMAGE_NAME}:${IMAGE_TAG}" .'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                sh '''
                docker push "${IMAGE_NAME}:${IMAGE_TAG}"
                '''
            }
        }
        stage('Trigger Deploy') {
            steps {
                build job: 'RobertaDeploy', wait: false, parameters: [
                string(name: 'ROBERTA_IMAGE_URL', value: "${IMAGE_NAME}:${IMAGE_TAG}")
                ]
            }
        }
    }

    post {
       always {
            sh 'docker image prune -a --force --filter "until=24h"'
       }
    }
}
