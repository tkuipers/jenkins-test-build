pipeline {
    triggers { pollSCM '*/1 * * * *' }
    agent any
    options {
        buildDiscarder(logRotator(daysToKeepStr: '15', artifactDaysToKeepStr: '7'))
    }
    
    stages {
        stage('Build Center') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://547222025036.dkr.ecr.ca-central-1.amazonaws.com/jenkins-test', 'ecr:ca-central-1:5cd84e3d-8930-464a-94a4-19461d2d4266') {
                        image = docker.build("jenkins-test:${env.GIT_COMMIT}")
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://547222025036.dkr.ecr.ca-central-1.amazonaws.com/jenkins-test', 'ecr:ca-central-1:5cd84e3d-8930-464a-94a4-19461d2d4266') {
                        image.push()
                    }
                }
            }
        }
    }
}