pipeline {
    agent any

    environment {
        EC2_IP = '35.178.251.8'
    }

    stages {
        stage ('fetch code') {
            steps {
                script {
                    echo "Pull source code from Git"
                    git branch: 'main', url: 'https://github.com/Kach07/Jenkin_deploy_on_UbuntuEC2.git'
                }
            }
        }
        
        stage ('deploy to EC2') {
            steps {
                script {
                    echo "deploying to shell-script to ec2"
                    def shellCmd = "bash ./websetup.sh"
                    sshagent (['ec2-server']) {
                        sh "scp -o StrictHostKeyChecking=no websetup.sh ubuntu@${EC2_IP}:/home/ubuntu"
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@${EC2_IP} ${shellCmd}"
                    }
                }
            }
        }
    }
}
