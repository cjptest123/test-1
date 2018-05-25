 repositoryName = "test"
pipeline {
	agent any
	stages {
	stage ('build') {
		steps {
			script {		
 	
             sh 'mvn clean package'
		}
	}
	}
	
    stage('Upload artifacts') {
            
            steps {
            script {
                def server = Artifactory.server ('test')
                               def uploadSpec  =  """{
                    "files": [
                {
                                  "pattern": "/var/lib/jenkins/workspace/test/target/cjp-1.3-SNAPSHOT.jar",
                  "target": "${repositoryName}" 
                }
                            ]
                      }"""

                        def buildInfo1 = server.upload(uploadSpec)
                        server.publishBuildInfo(buildInfo1)
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
		stage('ansibleTower')
        {
            steps
            {
                script
                {
                    
                    
                        ansibleTower credential: '',
                  //      extraVars: "tag: ${env.BUILD_NUMBER}",
                        importTowerLogs: false,
                        importWorkflowChildLogs: false,
                        inventory: 'Demo Inventory',
                        jobTags: '',
                        jobTemplate: 'Demo Job Template',
                        limit: '',
                        removeColor: false,
                        templateType: 'job',
                        towerServer: 'mahesh',
                        verbose: false
                    }
	    }
	}
		
	    }
}
		
	    

		
		
