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
        }
    }
		post
    {
             success
        {
                    mail to: 'cjptech12@gmail.com',
                     subject: "Succeded Pipeline: ${currentBuild.fullDisplayName}",
                     body: "Build got success check status @ ${env.BUILD_URL}"
             }
           failure
        {
                mail to: 'cjptech12@gmail.com',
                   subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                   body: "Something is wrong with ${env.BUILD_URL}"
            }
        }

	}
}
