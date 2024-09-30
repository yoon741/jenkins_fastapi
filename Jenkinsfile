pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('git scm update') {
            steps {
                git url: 'https://github.com/yoon741/jenkins_fastapi.git', branch: 'main'
            }
        }

        stage('docker build and push') {
            steps {
                sh '''
                docker build -t 43.201.49.130:8443/echo-ip .
                docker push 43.201.49.130:8443/echo-ip
                '''
            }
        }

        stage('Docker build and deploy') {
            steps {
                sh '''
                docker compose up --build -d
                '''
            }
        }
    }
}