pipeline {
    agent any
    stages {
        stage('Run') {
            steps {
                bat 'C:\\Users\\gohak\\AppData\\Local\\Python\\bin\\python.exe hello.py'
            }
        }
        stage('Test') {
            steps {
                bat 'C:\\Users\\gohak\\AppData\\Local\\Python\\bin\\python.exe -m pytest test_hello.py -v'
            }
        }
    }
    post {
        success { echo 'CI/CD Success' }
        failure { echo 'CI/CD Failure' }
    }
}
