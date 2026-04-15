pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'git-credentials', url: 'https://github.com/samatha-ux/addressbook-v1.git'
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
    }
}
