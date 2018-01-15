pipeline {
  agent any
  stages {
    stage('checking') {
      parallel {
        stage('checking') {
          steps {
            echo 'current directory is'
            sh 'pwd'
          }
        }
        stage('building infra') {
          steps {
            echo 'creating infra'
            sh '''cd /var/lib/jenkins/test1
cp -f /var/lib/jenkins/test1/chef/variables.tf ./ 
terraform init
terraform plan 
terraform apply -auto-approve

rm -f /var/lib/jenkins/test/variables.tf'''
          }
        }
        stage('post config ') {
          steps {
            echo 'configuring infra'
            sh '''cd /var/lib/jenkins/test1
cp -f /var/lib/jenkins/test1/a.txt chef
cp -f /var/lib/jenkins/test1/pro/variables.tf ./ 
sh anki.sh'''
          }
        }
      }
    }
  }
}