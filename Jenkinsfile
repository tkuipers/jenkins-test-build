/* Requires the Docker Pipeline plugin */
pipeline {
    triggers { pollSCM 'H/5 * * * *' }
    agent { 
        docker { 
            image 'maven:3.9.0-eclipse-temurin-11' 
        } 
    }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'
            }
        }
    }
}