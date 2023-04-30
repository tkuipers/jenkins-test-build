pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent { 
        docker { 
            image 'amazoncorretto:11-alpine3.17' 
        } 
    }
    stages {
        stage('prepare') {
            steps {
                sh 'sudo apk add docker'
            }
        }
        stage('build') {
            steps {
                sh 'sudo docker build -t bc:latest .'
            }
        }
        stage('push') {
            steps {
                sh 'sudo docker image ls'
            }
        }
    }
}