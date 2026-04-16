pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Correct syntax to clone your repository
                git url: 'https://github.com/samatha-ux/addressbook-v1.git', branch: 'master'
            }
        }
        
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
                // Replace 'your-aws-credentials-id' with your actual Jenkins Credentials ID
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
