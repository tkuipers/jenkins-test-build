pipeline {
    triggers { pollSCM '*/1 * * * *' }
    agent any
    options {
        buildDiscarder(logRotator(daysToKeepStr: '15', artifactDaysToKeepStr: '7'))
    }
    parameters{    
        string(
            defaultValue: env.GIT_COMMIT, 
            description: 'The commit you want to build', 
            name: 'COMMIT')
    }
    stages {
        stage("log params") {
            steps {
                echo "Hello ${params.COMMIT}"
                echo "Hello ${env.GIT_COMMIT}"
            }
        }
        stage('Checkout') {
            steps {
                echo "Hello ${env.GIT_COMMIT}"
                checkout([$class: 'GitSCM', 
                    branches: [[name: params.COMMIT]],
                    doGenerateSubmoduleConfigurations: false,
                    userRemoteConfigs: scm.userRemoteConfigs])
            }
        }
        stage('Build Center') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://547222025036.dkr.ecr.ca-central-1.amazonaws.com/jenkins-test', 'ecr:ca-central-1:5cd84e3d-8930-464a-94a4-19461d2d4266') {
                        image = docker.build("jenkins-test:${params.COMMIT}")
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