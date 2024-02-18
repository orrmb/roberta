pipeline {
    agent {
        docker {
        image 'orrmb/jenkinsagent'
        args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    options{parallelsAlwaysFailFast()}
    stages {
        stage('Unittest') {
            steps {
                sh '''
                pip install -r requirements.txt
                python3 -m pytest --junitxml results.xml tests
                '''
            }

            post {
                always {
                    junit allowEmptyResults: true, testResults: 'results.xml'
                }
            }
        }
        stage('Lint') {
            steps {
              sh 'python3 -m pylint -f parseable --reports=no *.py > pylint.log'
            }
            post {
                always {
                    sh 'cat pylint.log'
                    recordIssues (
                      enabledForFailure: true,
                      aggregatingResults: true,
                      tools: [pyLint(name: 'Pylint', pattern: '**/pylint.log')]
                    )
                }
            }
        }
        stage('Functional test') {
            steps {
                sh 'echo "testing"'
            }
        }
    }
}