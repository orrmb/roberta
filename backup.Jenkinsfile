pipeline {
    agent any


    environment {
        BUCKET_NAME = 'jenkins-orb'
        JENKINS_PATH  = '/var/lib/jenkins'
        BACKUPNAME = "backupforJENKINS_${BUILD_TIMESTAMP}.tar.gz"
        }

    stages {
        stage('Comppres to tar.gz') {
            steps {
                sh "sudo tar -czvf $BACKUPNAME $JENKINS_PATH"
            }
        }

        stage('Push to s3 Bucket'){
            steps{
                 sh "aws s3 cp $JENKINS_PATH/$BACKUPNAME s3://$BUCKET_NAME/"
                 sh 'Push to s3 bucket'
            }
        }

        stage('Remove the backup  from the server'){
            steps{
                sh "sudo rm $JENKINS_PATH/$BACKUPNAME"
                sh 'Remove Complete'
            }
        }
    }
  }


