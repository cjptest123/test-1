
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
      def server = Artifactory.server "http://34.229.203.138:8081/artifactory"
      def buildInfo = Artifactory.newBuildInfo()
      buildInfo.env.capture = true
      buildInfo.env.collect()

      def uploadSpec = """{
        "files": [
          {
            "pattern": "**/target/*.jar",
            "target": "example-repo-local"
          }, {
            "pattern": "**/target/*.pom",
            "target": "example-repo-local"
          }, {
            "pattern": "**/target/*.war",
            "target": "example-repo-local"
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


