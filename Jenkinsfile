pipeline {
    agent any
    stages {
        stage('Run') {
            steps {
                bat 'py hello.py'
            }
        }
        stage('Test') {
            steps {
                bat 'py -m pytest test_hello.py -v'
            }
        }
    }
    post {
        success { echo 'CI/CD Success' }
        failure { echo 'CI/CD Failure' }
    }
}
