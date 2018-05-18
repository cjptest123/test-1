
pipeline {
	agent any
	stages {
		

	stage ('build') {
		steps {
 	
             sh 'mvn clean package'
		}
	}
		
		stage ('upload') {
			steps {
    gitCommitStatus("upload") {
      def server = Artifactory.server "artifactory@ibsrv02"
      def buildInfo = Artifactory.newBuildInfo()
      buildInfo.env.capture = true
      buildInfo.env.collect()

      def uploadSpec = """{
        "files": [
          {
            "pattern": "**/target/*.jar",
            "target": "libs-snapshot-local"
          }, {
            "pattern": "**/target/*.pom",
            "target": "libs-snapshot-local"
          }, {
            "pattern": "**/target/*.war",
            "target": "libs-snapshot-local"
          }
        ]
      }"""
      // Upload to Artifactory.
      server.upload spec: uploadSpec, buildInfo: buildInfo

      buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
      // Publish build info.
      server.publishBuildInfo buildInfo
    }
  }
}
	}
}

