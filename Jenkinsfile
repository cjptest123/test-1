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
                                  "pattern": "/var/lib/jenkins/workspace/cdpipeline_test_master-Z4HEGPINOWF6XVURHR346BM3MVVQ2LZSSPIBEUUYT3DTJI3NXXDQ/target/cjp-1.0-SNAPSHOT.jar",
                  "target": "${repositoryName}/{env.BUILD_NUMBER}/" 
                }
                            ]
                      }"""

                        def buildInfo1 = server.upload(uploadSpec)
                        server.publishBuildInfo(buildInfo1)
              
                            }
        }
    }

	}
}
