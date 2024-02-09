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
                sh "tar -czvf $JENKINS_PATH$BACKUPNAME --absolute-names $JENKINS_PATH"
            }
        }

        stage('Push to s3 Bucket'){
            steps{
                 sh "aws s3 cp  $JENKINS_PATH$BACKUPNAME s3://$BUCKET_NAME/"
                 sh 'echo Push to s3 bucket'
            }
        }

        stage('Remove the backup  from the server'){
            steps{
                sh "sudo rm -f $JENKINS_PATH$BACKUPNAME"
                sh 'echo Remove Complete'
            }
        }
    }
    post{
        always {
            cleanWs(cleanWhenSuccess: true, deleteDirs: true)
       }
    }
  }

