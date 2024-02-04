pipeline {
    agent any

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
                sh 'docker build -t orrmb/roberta:0.0.$BUILD_NUMBER .'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                sh '''
                docker push orrmb/roberta:0.0.$BUILD_NUMBER
                '''
            }
        }
    }
    post {
       always {
            sh 'docker image prune -a --force --filter "until=24h"'
       }
    }
}
