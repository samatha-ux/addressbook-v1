pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/samatha-ux/addressbook-v1.git'
            }
        }
         stage('compilitation the code') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('code review') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Unit test') {
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
                profileName: 's3profile',// Must match the name in Manage Jenkins -> Configure System
                dontWaitForConcurrentBuildCompletion: false, 
                userMetadata: [], 
                consoleLogLevel: 'INFO', 
                pluginFailureResultConstraint: 'FAILURE', 
                dontSetBuildResultOnFailure: false,
                    entries: [[
                    bucket: 'aws-s3-bucket-1234567',
                    sourceFile: 'target/addressbook.war',
                    selectedRegion: 'us-east-1',
                    noUploadOnFailure: true,
                    managedArtifacts: true
                    ]]
                )            
            }
        }
    }
}
