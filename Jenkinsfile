pipeline {
    agent any
    
    stages {
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
        stage('Code Review') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        
        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('Code Coverage') {
            steps {
                sh 'mvn verify'
            }
        }

        stage('S3 Upload') {
            steps {
                // Using the ID from your screenshot: 'my-aws-id'
                withAWS(credentials: 'my-aws-id', region: 'us-east-1') {
                    s3Upload(
                        file: 'target/addressbook.war', 
                        bucket: 'samdevvishwa', 
                        path: 'addressbook.war'
                    )
                }
            }
        }
    }
}
