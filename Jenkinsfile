pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    environment {
        SONAR_HOST_URL = 'http://10.0.5.131:9000'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/shreevdeshmukh/sonar-scanning-examples.git'
            }
        }

        stage('Locate Maven Project') {
            steps {
                sh 'find . -name pom.xml'
            }
        }

        stage('Build and Analyze') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        cd sonar-scanner-maven
                        mvn clean verify sonar:sonar \
                          -Dsonar.host.url=$SONAR_HOST_URL
                    '''
                }
            }
        }
    }
}
