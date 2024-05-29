pipeline {
    agent any 
        environment {
            AWS_ACCESS_KEY_ID = credentials('AWS_CRED').AWS_ACCESS_KEY_ID
            AWS_SECRET_ACCESS_KEY = credentials('AWS_CRED').AWS_SECRET_ACCESS_KEY
        }
        parameters {      
            booleanParam( defaultValue: true, description: '',name: 'apply' )
             booleanParam( defaultValue: false, description: '',name: 'destroy' )
        }
        stages {
            stage('Checkout') {
                steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/lourash-hub/EKS-terraform-cluster.git']]])            
                  }
            }
            stage ('checking current dir'){
                steps {
                    sh 'pwd;ls;printenv'
                }
            }
            stage ('terraform init')
            {
                steps {
                    sh 'cd RDS;terraform init;pwd;terraform plan -var-file=rds-mysql.tfvars'
            }
            } 
            stage ('Terraform apply')
            {
                when {
                expression {  return params.apply == true  }
                }
                    steps {
                    sh 'cd RDS;terraform apply -var-file=rds-mysql.tfvars --auto-approve'
                }           

            }  
             stage ('Terraform destroy')
            {
                when {
                expression {  return params.destroy == true  }
                }
                    steps {
                    sh 'cd RDS;terraform destroy -var-file=rds-mysql.tfvars --auto-approve'
                }           

            }             
   
        }   
}
