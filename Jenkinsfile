pipeline {
    agent any
    stages {
        stage('Run') {
            steps {
                bat 'python hello.py'
            }
        }
        stage('Test') {
            steps {
                bat 'python -m pytest test_hello.py -v'
            }
        }
    }
    post {
        success { echo 'CI/CD Success' }
        failure { echo 'CI/CD Failure' }
    }
}
