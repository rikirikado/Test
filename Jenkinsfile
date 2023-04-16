pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3.8.3-openjdk-17'
                    // Run the container on the node specified at the
                    // top-level of the Pipeline, in the same workspace,
                    // rather than on a new node entirely:
                    reuseNode true
                }
            }
            steps {
                sh 'mvn --version'
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {

            agent { node { label 'Built-In Node' } }
            steps {
                sh 'ls -l target'
      	        sh 'docker build -t test-app:latest .'
            }
        }
    }
}