pipeline {
    agent any
          environment {
    Secret_key = credentials('Secret_access_key')
    Access_key = credentials('Access_key_ID')
     }
    options {
        skipStagesAfterUnstable()
    }
    stages {  
       stage('configure aws') {
            steps{ 
                sh '''
                aws configure set aws_access_key_id ${Access_key}
                aws configure set aws_secret_access_key ${Secret_key}
                aws configure set default.region us-west-1
                '''
                }
          }
          stage('get master node public ip') {
            steps{                  
                sh '''
                PUBLIC_IP=$(aws ec2 describe-instances --instance-ids i-0d2817565eeac7442 --query "Reservations[0].Instances[0].PublicIpAddress" --output text)
                echo $PUBLIC_IP > ip.txt
                ssh-keyscan -H $PUBLIC_IP >> ~/.ssh/known_hosts
                '''
                stash name: 'ip', includes: 'ip.txt'                          
               }
            }
        stage('connect to the master node') {
            steps{ 
                unstash 'ip'
                sh '''
                PUBLIC_IP=$(cat ip.txt)
                aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin 333082661382.dkr.ecr.us-west-1.amazonaws.com
                scp -i ~/test-servers-key.pem file.txt ubuntu@$PUBLIC_IP:/home/ubuntu
                ssh -i ~/test-servers-key.pem ubuntu@$PUBLIC_IP ./home/ubuntu/kube_config/jenkins_CD.sh
                '''
            }
        }
    }
}
