pipeline {
    agent any

    tools {
        maven "Maven"
        jdk "JDK17"
    }

    stages {
        stage('Fetch code') {
            steps {
                git branch: 'atom', url: 'https://github.com/hkhcoder/vprofile-project.git'
            }
        }

        

        stage('Build') {
            steps {
                sh 'mvn install -DskipTests'
            }

            post {
                success {
                    echo "Archiving the artifacts"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Unit test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Checkstyle Analysis'){
          steps{
            sh 'mvn checkstyle:checkstyle'

          }
        }

        stage("Sonar Code Analysis"){
          steps {
            withSonarQubeEnv("sonar"){
              sh 'mvn clean package sonar:sonar'
            }
          }
        }
    }
}