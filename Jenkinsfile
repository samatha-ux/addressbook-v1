pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'adcbec07-694e-432f-a4d6-0592ad377cde', url: 'https://github.com/samatha-ux/addressbook-v1.git'
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
                    bucket: 'samdevvishwa',
                    file: 'target/addressbook.war',
                    acl: 'Private'
                )
            }
        }
       
                
        
    
    }
}
