pipeline {
    agent any
    stages {
        stage('checkout') { 
            steps {
                 
            git 'https://github.com/cjpcloud/warrepo.git'
}
        }
        stage('build') { 
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') { 
            steps {
                s3Upload consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'jenkins369', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**', storageClass: 'STANDARD', uploadFromSlave: true, useServerSideEncryption: false]], pluginFailureResultConstraint: 'SUCCESS', profileName: 'bucket', userMetadata: []
            }
        }
    }
}
