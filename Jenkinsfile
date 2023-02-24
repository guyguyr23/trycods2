/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
      environment {
    MY_CREDENTIAL = credentials('guy')
     } 
    stages {
        stage('build') {
            steps{ 
                sh '''
                sh "echo My credential is $MY_CREDENTIAL"
                #ssh -i ~/test-servers-key.pem ubuntu@54.67.54.114 kubectl apply -f kube_config/deployment.yml
                '''
            }
        }
    }
}

