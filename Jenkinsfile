pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent any
    stages {
        stage('build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('push') {
            steps {
                sh 'docker image ls'
            }
        }
    }
}