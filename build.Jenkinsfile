pipeline {
    agent any

        stages {
        stage('Dcoker hub login') {
            steps {
                withCredentials([string(credentialsId: 'Docker_hub', usernameVariable : 'USER', passwordVariable:'PASS')]){
                docker login -u $USER -p $PASS
                }
            }
        }
    }

    stages {
        stage('Build Dcoker Image') {
            steps {
                docker build -t orrmb/roberta .
            }
        }
    }
        stages {
        stage('Push Docker Image to DcokerHub') {
            steps {
                docker push orrmb/roberta
            }
        }
    }
}
