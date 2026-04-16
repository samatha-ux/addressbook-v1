pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Code coverage') {
            steps {
                sh 'mvn verify'
            }
        }
        stage('s3 bucket storing') {
            steps {
                s3Upload(
                    profileName: 'S3-Credentials', 
                    consoleLogLevel: 'INFO', 
                    dontSetBuildResultOnFailure: false, 
                    dontWaitForConcurrentBuildCompletion: false, 
                    pluginFailureResultConstraint: 'FAILURE', 
                    userMetadata: [], 
                    entries: [[
                        bucket: 'samdevvishwa', 
                        selectedRegion: 'us-east-1', 
                        sourceFile: 'target/addressbook.war', 
                        noUploadOnFailure: true
                    ]]
                )
            }
        }
    }
}
