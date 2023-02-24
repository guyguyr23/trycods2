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
                PUBLIC_IP=$(aws ec2 describe-instances --instance-ids i-0d2817565eeac7442 --query "Reservations[0].Instances[0].PublicIpAddress" --output text)
                ssh-keyscan -H $PUBLIC_IP >> ~/.ssh/known_hosts
                echo ok
                ssh -i ~/test-servers-key.pem ubuntu@54.67.54.114 sudo kubectl apply -f kube_config/deployment.yml
                '''
            }
        }
    }
}

