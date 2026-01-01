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
                script {
                    echo "Generating Security Report..."
                    
                    // 1. توليد تقرير HTML (لن يفشل الـ build هنا مهما كانت الثغرات)
                    // قمنا بتحميل ملف التنسيق html.tpl ليكون التقرير أنيقاً
                    sh "trivy image --format template --template '@/usr/local/share/trivy/templates/html.tpl' -o report.html ${IMAGE_NAME}:latest"
                    
                    // 2. الفحص الفعلي الذي يحدد نجاح أو فشل الـ Build (فقط للـ CRITICAL)
                    sh "trivy image --severity CRITICAL --exit-code 1 ${IMAGE_NAME}:latest"
                }
            }
            post {
                always {
                    // نشر التقرير ليظهر في واجهة جينكينز
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: '.',
                        reportFiles: 'report.html',
                        reportName: 'Trivy Security Report',
                        reportTitles: 'Vulnerability Scan Results'
                    ])
                }
            }
        }

//        stage('Security Scan (Trivy)') {
//            steps {
//                echo "Running Vulnerability Scan..."
                // هنا نقوم بفحص الصورة. 
                // --severity HIGH,CRITICAL يعني ابحث عن الثغرات العالية والخطيرة فقط.
                // --exit-code 1 يعني أفشل الـ Pipeline إذا وجدت أي ثغرة.
//                sh "trivy image --severity CRITICAL --exit-code 1 ${IMAGE_NAME}:latest"
//            }
//        }
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
