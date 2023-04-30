pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent { 
        docker { 
            image 'amazoncorretto:11' 
        } 
    }
    stages {
        stage('prepare') {
            steps {
                sh 'apk add docker'
            }
        },
        stage('build') {
            steps {
                sh 'docker build -t bc:latest .'
            }
        },
        stage('push') {
            steps {
                sh 'docker image ls'
            }
        }
    }
}