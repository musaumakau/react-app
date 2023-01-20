pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-5936')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/musaumakau/react-app.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t 5936/react-app:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push 5936/react-app:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

