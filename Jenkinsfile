
pipeline {
	agent any
	stages {
		

	stage ('cjpdemo - Checkout') {
		steps {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'e7092d59-2ba1-4288-8a74-62219298460d', url: 'https://github.com/cjpcloud/jarrepo.git']]]) 
	}
	}
	stage ('cjpdemo - Build') {
		
		steps {
 	
	withMaven(maven: 'mvn') { 
		git 'https://github.com/cdpipeline/test.git'
 		 //if(isUnix()) {
 				// sh "mvn clean package " 
		//	} else { 
 		//	 	bat "mvn clean package "
		//	 fi
		//	} 
 		} 
	}
	}
	}
}

