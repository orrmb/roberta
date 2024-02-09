pipeline {
    agent any


    environment {
        BUCKET_NAME = 'jenkins-orb'
        JENKINS_PATH  = '/var/lib/jenkins/'
        BACKUPNAME = "backupforJENKINS_${BUILD_NUMBER}.tar.gz"
        }

    stages {
        stage('Comppres to tar.gz') {
            steps {
                sh "tar -czvf $BACKUPNAME --absolute-names $JENKINS_PATH"
            }
        }

        stage('Push to s3 Bucket'){
            steps{
                 sh "aws s3 cp $JENKINS_PATH$BACKUPNAME s3://$BUCKET_NAME/"
                 sh 'Push to s3 bucket'
            }
        }

        stage('Remove the backup  from the server'){
            steps{
                sh "rm $JENKINS_PATH$BACKUPNAME"
                sh 'Remove Complete'
            }
        }
    }
    post{
        always {
            cleanWs(cleanWhenSuccess: true, deleteDirs: true)
       }
    }
  }


