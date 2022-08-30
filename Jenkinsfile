pipeline {
    //agent {label 'linux'}
    agent any
     environment {
                
                GOOGLE_PROJECT_ID = 'burner-athwatho'
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
                        sh 'sudo yum install kubectl -y'
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
                withCredentials([file(credentialsId: 'gcp-key', variable: 'GCP_KEY')]) {
                    sh("gcloud auth activate-service-account --key-file=${GCP_KEY}")
                    sh("gcloud config set project ${GOOGLE_PROJECT_ID}")
                }
                    sh("sudo terraform plan")
                    sh("sudo terraform apply -auto-approve")
                
            }
        }
        
        stage('Deployment') {
            steps {
                
                echo 'deployed'
              
            }
        }
    }
}
