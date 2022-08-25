pipeline {
    //agent {label 'linux'}
    agent {
        node {
            label 'Built-in Node'
            customWorkspace '/tmp/myjenkinsnfs/my_workspace/my_terraform'
        }
    }
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
                        sh 'terraform init'
                        sh 'terraform fmt'
                    } catch(Exception e) {
                        echo "Exception received" + e
                        } 
                }

            }
        }
        stage('Validate') {
            steps {
                sh 'terraform validate'
                
            }
        }
        stage('Plan') {
            steps {
                
                sh 'terraform plan'
            }
        }
        
        stage('Deployment') {
            steps {
                
                sh 'terraform apply -auto-approve'
              
            }
        }
    }
}
