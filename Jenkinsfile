pipeline {
    agent any
    stages {
        stage('Install') {
            steps {
                bat 'C:\\Users\\gohak\\AppData\\Local\\Python\\bin\\python.exe -m pip install -r requirements.txt'
            }
        }
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
        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                    bat '''
                        curl -s -X POST ^
                        -H "Authorization: token %GITHUB_TOKEN%" ^
                        -H "Content-Type: application/json" ^
                        -d "{\\"tag_name\\": \\"v%BUILD_NUMBER%\\", \\"name\\": \\"Release v%BUILD_NUMBER%\\", \\"body\\": \\"Auto release by Jenkins\\"}" ^
                        https://api.github.com/repos/gohakushi1118/Test-CICD/releases
                    '''
                }
            }
        }
    }
    post {
        success { echo 'CI/CD Success' }
        failure { echo 'CI/CD Failure' }
    }
}
