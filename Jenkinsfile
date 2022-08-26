pipeline {
    //agent {label 'linux'}
    agent any
    
    stages {
        stage('Git Checkout') {
        steps {
            git branch: 'master',
                credentialsId: 'jenkins-github',
                url: 'https://github.com/AtharvaWathodkar/my-tarraform-google-gkr.git'
            }
        }
        stage('Terraform init') {
            steps {
                script {
                    try {
                        //echo "${my_env}"
                        sh 'sudo terraform init'
                        sh 'sudo terraform fmt'
                    } catch(Exception e) {
                        echo "Exception received" + e
                        } 
                }

            }
        }
        stage('Validate') {
            steps {
                sh 'sudo terraform validate'
                
            }
        }
        stage('Plan') {
            steps {
                
                sh 'sudo terraform plan'
            }
        }
        
        stage('Deployment') {
            steps {
                
                sh 'sudo terraform apply -auto-approve'
              
            }
        }
    }
}
