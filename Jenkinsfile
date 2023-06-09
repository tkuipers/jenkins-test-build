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
        stage('Checkout') {
            steps {
                script {
                    commit = env.GIT_COMMIT
                    if(params.COMMIT != null && params.COMMIT != '') {
                        commit = params.COMMIT
                    }
                }
                checkout([$class: 'GitSCM', 
                    branches: [[name: commit]],
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
                        echo "Tagging image: jenkins-test:${commit}"
                        image = docker.build("jenkins-test:${commit}")
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