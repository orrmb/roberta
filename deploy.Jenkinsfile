pipeline {
    agent {
        docker {
        image 'orrmb/jenkinsagent'
        args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    parameters { string(name: 'ROBERTA_IMAGE_URL', defaultValue: '', description: '') }

    stages {
        stage('Deploy') {
            steps {
                // complete this code to deploy to real k8s cluster
                sh "echo $ROBERTA_IMAGE_URL"
            }
        }
    }
}
