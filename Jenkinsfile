/* Requires the Docker Pipeline plugin */
pipeline {
    agent any 
    environment {
        AWS_ACCESS_KEY_ID = credentials("AWS_ACCESS_KEY_ID")
        AWS_SECRET_ACCESS_KEY = credentials("AWS_SECRET_KEY_ID")
    }
    stages {
        stage('Remote SSH') {
            steps{ 
                sh '''
                aws configure set aws_access_key_id ${AWS_ACCESS_KEY_ID}
                aws configure set aws_secret_access_key ${AWS_SECRET_ACCESS_KEY}
                aws configure set default.region us-west-1
                PUBLIC_IP=$(aws ec2 describe-instances --instance-ids i-0d2817565eeac7442 --query "Reservations[0].Instances[0].PublicIpAddress" --output text)
                ssh-keyscan -H $PUBLIC_IP >> ~/.ssh/known_hosts
                ssh -T -i ~/test-servers-key.pem ubuntu@$PUBLIC_IP whoami
                '''
            }
        }
    }
}

