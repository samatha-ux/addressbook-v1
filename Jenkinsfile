pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                git credentialsId: 'git', url: 'https://github.com'
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
                // Ensure the 'Pipeline: AWS Steps' plugin is installed for s3Upload
                // 'file' is the path to your artifact relative to the workspace
                s3Upload(file: 'target/addressbook.war', bucket: 'samdevvishwa', path: 'addressbook.war')
            }
        }
    } // Closes stages
} // Closes pipeline
