repositoryName = "demo"
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
                                  "pattern": "/var/lib/jenkins/workspace/cdpipeline_test_master-Z4HEGPINOWF6XVURHR346BM3MVVQ2LZSSPIBEUUYT3DTJI3NXXDQ/target/cjp-1.1-SNAPSHOT.jar",
                  "target": "${repositoryName}" 
                }
                            ]
                      }"""

                        def buildInfo1 = server.upload(uploadSpec)
                        server.publishBuildInfo(buildInfo1)
	    
	    }		    
  post
    {
         success
        {
            script
            {
                     mail to: 'sujith918@gmail.com',
                     subject: "Build + Condition Pass",
                     body: "Build got success check status @ ${env.BUILD_URL}"
                
            }
        }
           failure
        {
                script
            {
               
                    mail to: 'sujith918@gmail.com',
                     subject: "Build fail + Condition Pass",
                     body: "Build got success check status @ ${env.BUILD_URL}"
                 
            }
        }
    }
                            
        }
    }
		


	}
}
		

