pipeline {
    agent any

    stages {

        stage('git checkout') {
            steps {
                git credentialsId: 'git-credentials', 
                    url: 'https://github.com/samatha-ux/addressbook-v1.git'
            }
        }

        stage('compilation the code') {
            steps {
                sh 'mvn clean compile'
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

        stage('Code Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Code coverage') {
            steps {
                sh 'mvn verify'
            }
        }

        stage('S3 bucket storing') {
            steps {
                withAWS(credentials: 'aws-credentials-id', region: 'us-east-1') {
                    s3Upload(
                        entries: [
                            [
                                sourceFile: 'target/*.war',
                                bucket: 'declarative1',
                                accessControlList: 'Private'
                            ]
                        ]
                    )
                }
            }
        }
    }
}
