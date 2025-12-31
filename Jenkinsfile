pipeline {
    agent any
    environment {
        IMAGE_NAME = "my-secure-app"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }
        stage('Security Scan (Trivy)') {
            steps {
                echo "Running Vulnerability Scan..."
                // هنا نقوم بفحص الصورة. 
                // --severity HIGH,CRITICAL يعني ابحث عن الثغرات العالية والخطيرة فقط.
                // --exit-code 1 يعني أفشل الـ Pipeline إذا وجدت أي ثغرة.
                sh "trivy image --severity HIGH,CRITICAL --exit-code 1 ${IMAGE_NAME}:latest"
            }
        }
        stage('Deploy') {
            steps {
                // لن يصل جينكينز لهذه المرحلة إذا فشل الفحص الأمني أعلاه
                sh """
                    docker rm -f secure-app-container || true
                    docker run -d --name secure-app-container -p 3000:3000 ${IMAGE_NAME}:latest
                """
            }
        }
    }
}
