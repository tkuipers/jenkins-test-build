pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent any
    stages {
        stage('Build Center') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry('547222025036.dkr.ecr.ca-central-1.amazonaws.com/jenkins-test', 'ecr:ca-central-1:5cd84e3d-8930-464a-94a4-19461d2d4266') {

                        // build image
                        def customImage = docker.build("center:${env.BUILD_ID}")

                        // push image
                        customImage.push()
                    }
                }
            }
        }
    }
}