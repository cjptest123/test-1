// repositoryName = "demo"
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
                                  "pattern": "C:\Users\Administrator\Documents\jenkins\workspace\test\target\** ",
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
    
		
	    }

	}
		
		
