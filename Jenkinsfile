
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
                def server = Artifactory.server ('mahiJFrog')
                if (isMaster){
                def uploadSpec  =  """{
                    "files": [
                {
                                  "pattern": "${repositoryName}-1.0.${env.BUILD_NUMBER}.tar",
                  "target": "${repositoryName}/{env.BUILD_NUMBER}/"
                }
                            ]
                      }"""

                        def buildInfo1 = server.upload(uploadSpec)
                        server.publishBuildInfo(buildInfo1)
                }
                else{
                def uploadSpec = """{
                "files": [
                   {
                   "pattern": "${repositoryName}-1.0.${env.BUILD_NUMBER}.tar",
                   "target": "${repositoryName}/"
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
}
