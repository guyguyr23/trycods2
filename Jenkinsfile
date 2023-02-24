/* Requires the Docker Pipeline plugin */
pipeline {
    agent any 
    stages {
        stage('build') {
            steps{ 
                sh '''
                echo ok
                ssh -i ~/test-servers-key.pem ubuntu@54.67.54.114 whoami
                '''
            }
        }
    }
}

