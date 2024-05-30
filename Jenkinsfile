pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select the action to perform')
    }
    stages {
        stage('Deploy VPC') {
            steps {
                echo 'Deploying VPC..'
                build job: 'deploy-vpc', parameters: [string(name: 'ACTION', value: params.ACTION)]
            }
        }
        stage('Deploy EKS') {
            steps {
                echo 'Deploying EKS..'
                build job: 'deploy-eks', parameters: [string(name: 'ACTION', value: params.ACTION)]
            }
        }
        stage('Deploy RDS') {
            steps {
                echo 'Deploying RDS....'
                build job: 'deploy-rds', parameters: [string(name: 'ACTION', value: params.ACTION)]
            }
        }
    }
}