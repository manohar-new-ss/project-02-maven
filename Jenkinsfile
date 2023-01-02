# ansible, using password file, etc trying the pipeline
# jenkins file to initiate the ansible to install httpd using yaml
pipeline{
    agent any
tools{
        maven 'maven.3.8.4'
    }
    options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '3', numToKeepStr: '1')
}

    environment{
        
            Httpd='installhttpd.yaml'
    }
    stages{
        stage('CODE-CHECKOUT'){
            steps{
                git branch: 'development', credentialsId: 'git-credentials', url: 'https://github.com/manohar-new-ss/project-02-maven.git'
            }
        }
        
        stage('ansible-playbook check and dry run'){
            steps{
                
                withCredentials([string(credentialsId: 'vaultpass', variable: 'vaultpass')]) {
                    
                sh "echo $vaultpass > passwrdfile" 
        
                sh "ansible-playbook $Httpd --extra-vars server=httpd  --vault-password-file=passwrdfile  --check"
                
                sleep 2
            
                sh " rm passwrdfile"
                    
                }
            }
        }
    }
}
