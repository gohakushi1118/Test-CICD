# CI/CD test
Just a Test :)

```
pipeline {
    agent any // 在任何節點執行

    environment {
        MY_VAR = '' // 環境變數
    }

    stages {
        stage('Build') { // 建立環境
            steps {
                bat
            }
        }

        stage('Test') { // 軟體測試
            steps {
                bat
            }
        }

        stage('Deploy') { // 部署
            when {
                branch 'main'
            }
            steps {
                bat
            }
        }
    post { // 執行後動作
        success { echo 'CI/CD Success' }
        failure { echo 'CI/CD Failure' }
    }
}
```