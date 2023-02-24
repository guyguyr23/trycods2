/* Requires the Docker Pipeline plugin */
pipeline {
    agent any
      environment {
    Secret_key = credentials('Secret_access_key')
    Access_key = credentials('Access_key_ID')
     } 
    stages {
        stage('build') {
            steps{ 
                sh '''
                aws configure set aws_access_key_id ${Access_key}
                aws configure set aws_secret_access_key ${Secret_key}
                aws configure set default.region us-west-1
                echo ok
                #ssh -i ~/test-servers-key.pem ubuntu@54.67.54.114 kubectl apply -f kube_config/deployment.yml
                '''
            }
        }
    }
}

