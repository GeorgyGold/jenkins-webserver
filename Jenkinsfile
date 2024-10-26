pipeline {
    agent any
    stages {

        // Init stage 
        stage('Terraform Init') {
            steps {
                    sh 'terraform init -reconfigure'
                    sh 'terraform init -migrate-state'
                    sh 'terraform fmt'
            }
        }

        // Plan stage 
        stage('Terraform Plan') {
            steps {
                    sh 'terraform plan'
            }
        }

        // Apply stage 
        stage('Terraform Apply') {
            steps {

                    sh 'terraform apply -auto-approve'
            }
        }

        // Approval stage 
        stage ("Destroy approval") {
            steps {
                    echo "Taking approval from DEV Manager for QA Deployment"
                    timeout(time: 7, unit: 'DAYS') {
                    input message: 'Do you want to Destroy the Infra', submitter: 'admin'
                    }
                }    
            }   

        // Destroy stage               
        stage('Terraform Destroy') {
            steps {
                    sh 'terraform destroy -auto-approve'
            }
        }        
    }    
}
