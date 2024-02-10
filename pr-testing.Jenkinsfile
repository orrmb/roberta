pipeline {
    agent any

    stages {
        stage('Unittest') {
            steps {
                sh 'echo "testing"'
                sh 'python test_cache.py'
            }
        }
        stage('Lint') {
            steps {
                sh 'echo "linting"'
            }
        }
        stage('Functional test') {
            steps {
                sh 'echo "testing"'
            }
        }
    }
}