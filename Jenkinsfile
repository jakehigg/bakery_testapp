pipeline {
    agent any 

    stages {
        stage('Git Packer Template') { 
            steps { 
                sh 'rm -rvf bakery_testapp'
                sh 'git clone https://github.com/jakehigg/bakery_testapp.git' 
            }
        }
        stage('Bake') {
            steps {
                withCredentials([string(credentialsId: 'aws_access_key', variable: 'aws_access_key')]) {
                withCredentials([string(credentialsId: 'aws_secret_key', variable: 'aws_secret_key')]) {
                sh '''
                packer build -var "aws_access_key=$aws_access_key" -var "aws_secret_key=$aws_secret_key" -var "source_ami=ami-da05a4a0" -var "vpc_id=vpc-04bea57d" -var "subnet_id=subnet-86bb84aa" bakery_testapp/packer/bakery.json
                '''
                }}
               
                }
            }
        }
    }

