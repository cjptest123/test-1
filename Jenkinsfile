
		
	    
pipeline {
    agent any 
    stages {
        stage('Checkout') { 
            steps {
                script {
                 git 'https://github.com/cjpcloud/warrepo.git'

            }
        }
        }
        stage('Build') { 
            steps {
                script {
                sh 'mvn clean package'
            }
        }
        }
        stage ('deploy') {
            steps {
                script {
                s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'jenkins369', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**', storageClass: 'STANDARD', uploadFromSlave: true, useServerSideEncryption: false]], pluginFailureResultConstraint: 'SUCCESS', profileName: 's3bucket', userMetadata: []
            }
        }
        
post
    {
         success
        {
            script
            {
            
		    mail to: 'cjptech12@gmail.com',
                     subject: "Build + Condition Pass",
                     body: "Build got success check status @ ${env.BUILD_URL}"
                
            }
	}
        
          failure
	   {
		   script
		   {
                mail to: 'cjptech12@gmail.com',
                     subject: "Build fail + Condition Pass",
                     body: "Build got success check status @ ${env.BUILD_URL}"
                 
            }
        }
    }
                            
        }
    
    }
}
		
		
