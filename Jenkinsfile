pipeline {
    agent any
    
    environment {
        DOCKERHUB_SECRETS = credentials('dockerhub')
        IMAGE_NAME = "yoon741/jenkins_jodejs3"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('clone from SCM') {
            steps {
                git url: 'https://github.com/yoon741/jenkins_fastapi.git', branch: 'main'
            }
        }
        
        stage('Docker Building Node.js App') {
            steps {
                sh '''
                docker compose build
                '''
            }
        }
        
        stage('Logging into Docker Hub') {
            steps {
                sh '''
                echo ${DOCKERHUB_SECRETS_PSW} | docker login -u ${DOCKERHUB_SECRETS_USR} --password-stdin
                '''
            }
        }
        
        stage('Pushing Docker image to Docker Hub') {
            steps {
                sh '''
                docker tag yoon741/nodejs-app ${IMAGE_NAME}:${IMAGE_TAG}
                docker push ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
        
        stage('Docker Hub logout') {
            steps {
                sh '''
                docker logout
                '''
            }
        }
    }
}
