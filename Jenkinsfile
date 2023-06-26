pipeline {
    agent {
        label 'docker-remote'
    }
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
                withSonarQubeEnv(installationName: 'sq1') {
                    sh 'mvn clean sonar:sonar'
                }
            }
        }

        


        stage('Docker Build') {
            steps {
                sh 'docker build -t demp-test-app:latest .'
            }
        }
    }
}
