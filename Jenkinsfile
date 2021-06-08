// Powered by Infostretch 

timestamps {

node () {

	stage ('app-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'cynthiaPF', url: 'https://github.com/cynthiaPF/jenkins-sample.git']]]) 
	}
	/*
	stage ('app-IC - Build') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 		} 
	}
	*/
	stage('Quality check') {
	withSonarQubeEnv('Sonar') {
		bat "mvn sonar:sonar"
		}
	}
	stage ('app-IC - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'cynthia.peraltafonseca@gmail.com', sendToIndividuals: false])
 
	}
}
}
