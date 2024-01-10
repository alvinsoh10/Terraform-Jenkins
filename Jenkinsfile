pipeline {

    agent any
     stages {
        stage ('Checkout'){
            steps{
                script{
                    dir('terraform'){
                        sh("git clone --depth 1 --no-checkout https://github.com/alvinsoh10/Terraform-AWS.git")
                        sh 'pwd; cd Terraform-AWS'
                        sh 'git sparse-checkout init --cone'
                        sh 'git sparse-checkout set Terraform'
                        sh 'git checkout'

                    }
                }
            }
        }
        stage('Plan'){
            steps{
                sh 'pwd;cd terraform/ ; terraform init'
                sh "pwd;cd terraform/ ; terraform plan -out tfplan"
                sh 'pwd;cd terraform/ ; terraform show -no-color tfplan > tfplan.txt'
            }
        }

        stage('Build'){
            steps{
                sh "pwd;cd terraform/ ; terraform apply -input=false tfplan"
            }
        }
     }
}