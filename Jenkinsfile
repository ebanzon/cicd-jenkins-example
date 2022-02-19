pipeline {
	agent any
	
	stages {
		stage ('Build') {
			steps {
				withMaven(maven: 'maven_3_5_0') {
					sh 'mvn clean compile'
				}
			}
		}
		
		stage ('Deploy') {
			withCredentials([[$class		: 'UsernamePasswordMultiBinding',
							  credentialsId	: 'PCF_LOGIN',
							  usernameVariable: 'USERNAME',
							  passwordVariable: 'PASSWORD']]) {
				sh 'cf login -a https://api.us-south.cf.cloud.ibm.com -u $USERNAME -p $PASSWORD'
				sh 'cf push'			  
			}
		}
		
	}
}