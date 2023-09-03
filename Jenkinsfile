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
	
	stage('Code Scan'){
		withSonarQubeEnv(credentialsId: 'SonarQubeCreds') {
			sh "${sonarHome}/bin/sonar-scanner"
		}
		
	}
	
	stage('Code Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://54.197.62.94:8080/')], contextPath: 'Planview', onFailure: false, war: 'target/*.war'
	}
	}
}
