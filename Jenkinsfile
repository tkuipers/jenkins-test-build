pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent { 
        docker { 
            image 'amazoncorretto:11-alpine3.17' 
            args '-u root --privileged'
        } 
    }
    stages {
        stage('prepare') {
            steps {
                sh 'apk add docker-cli openrc'

            }
        }
        stage('build') {
            steps {
                sh 'docker build -t bc:latest .'
            }
        }
        stage('push') {
            steps {
                sh 'docker image ls'
            }
        }
    }
}