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

        stage('Unit test') {
            steps {
                sh 'mvn test'
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
    }
}