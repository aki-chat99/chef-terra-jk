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
            sh '''cd /var/lib/jenkins/test2
cp -f /var/lib/jenkins/test2/chef/variables.tf ./ 
terraform init
terraform plan 
terraform apply -auto-approve

rm -f /var/lib/jenkins/test/variables.tf'''
          }
        }
        stage('config infra') {
          steps {
            echo 'config infra'
            sh '''cd /var/lib/jenkins/test1/chef
cp -f /var/lib/jenkins/test1/a.txt chef
sh anki.sh'''
          }
        }
      }
    }
  }
}