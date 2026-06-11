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

```
 ┌─────────────────── CI ───────────────────┐ ┌──────────── CD ────────────┐
 Push → Checkout → Build → Test → Artifact  →  Staging → (核可) → Prod → 監控
                            │                                            │
                          失敗就停止並通知                          出事就回滾
```

| 面向 | 沒 Docker | 有 Docker |
|------|-----------|-----------|
| 思維 | 在機器上**裝環境再跑程式** | 把**程式 + 環境一起打包成 image**，到處跑同一個 image |
| 環境來源 | 依賴 CI 機器本機已裝的工具（如 `C:\...\python.exe`） | 寫在 `Dockerfile`，環境跟著 image 走 |
| 一致性 | 容易「在我機器上會動」 | 開發 / 測試 / 正式跑**完全同一個 image** |
| 產出物 | 通常沒有，或散落的檔案 | **image** 本身就是不可變的 artifact |
| 回滾 | 困難，要重裝環境 | 換個 image tag 即可精準回滾 |
