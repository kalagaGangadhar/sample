pipeline {
    agent {
        node {
            label 'slave1'
        }
    }
    stages {
        stage('Git Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github access', url: 'https://github.com/kalagaGangadhar/sample.git']]])
                sh 'pwd'
            }
        }
        stage('Terraform init') {
            steps {
                sh 'pwd'
                sh 'terraform init'
            }
        }
        stage('Terraform validate') {
            steps {
                sh 'pwd'
                sh 'terraform validate'
            }
        }
        stage('Terraform plan') {
            steps {
                sh 'pwd'
                sh 'terraform plan'
            }
        }
        stage('Terraform apply/destroy') {
            parallel {
                stage('Terraform apply') {
                    when {
                        expression {
                            "$State" == "apply"
                        }
                    }
                    steps {
                        sh 'pwd'
                        sh 'terraform apply --auto-approve'
                    }
                }
                stage('Terraform destroy') {
                    when {
                        expression {
                            "$State" == "destroy"
                        }
                    }
                    steps {
                        sh 'pwd'
                        sh 'terraform destroy --auto-approve'
                    }
                }
            }
        }
    }
}