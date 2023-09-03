pipeline{
    agent any
    tools{
        maven 'maven'
    }

    stages{
        stage('Code Checkout'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vprasadreddy/jenkins-tomcat-deployment.git']])
            }
        }
	
	stage('Maven Build'){
		sh 'mvn clean install'
	}
	stage('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
	
	stage('Tomcat Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://54.145.49.155:8080/')], contextPath: null, onFailure: false, war: '   **/*.war'
	}
	}
}
