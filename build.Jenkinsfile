pipeline {
    agent any

    stages {
        stage('Docker Hub login') {
            steps {
                withCredentials([string(credentialsId: 'Docker_Hub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh "docker login -u $USER -p $PASS"
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t orrmb/roberta .'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                sh 'docker push orrmb/roberta'
            }
        }
    }
}
