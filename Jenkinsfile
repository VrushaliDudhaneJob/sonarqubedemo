
pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
    }

    environment {
        SONAR_HOST_URL = 'http://13.233.149.174:9000'
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {

        stage('Checkout') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/VrushaliDudhaneJob/sonarqubedemo.git'
                )
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Code Analysis') {
            steps {
                sh '''
                    mvn sonar:sonar \
                        -Dsonar.projectKey=my-project \
                        -Dsonar.projectName=my-project \
                        -Dsonar.host.url=$SONAR_HOST_URL \
                        -Dsonar.token=$SONAR_TOKEN
                '''
            }
        }
    }
}
