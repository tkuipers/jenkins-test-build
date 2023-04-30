pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent { 
        docker.withRegistry("547222025036.dkr.ecr.ca-central-1.amazonaws.com/jenkins-test", "ecr:ca-central-1:5cd84e3d-8930-464a-94a4-19461d2d4266") { 
            image 'amazoncorretto:11-alpine3.17' 
            args '-u root --privileged'
        } 
    }
    stages {
        stage('prepare') {
            steps {
                sh 'apk add docker openrc'

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