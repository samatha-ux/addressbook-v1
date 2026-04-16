pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                // Correct syntax to clone a repository
                git 'https://github.com/samatha-ux/addressbook-v1.git'
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
                // Requires 'Pipeline: AWS Steps' plugin
                s3Upload(file: 'target/addressbook.war', bucket: 'samdevvishwa', path: 'addressbook.war')
            }
        }
    } 
}
