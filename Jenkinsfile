pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage('Code Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vprasadreddy/jenkins-tomcat-deployment.git']])
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }

        stage('Tomcat Deployment') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.145.49.155:8080/')], contextPath: null, onFailure: false, war: '   **/*.war'
            }
        }
    }
}
