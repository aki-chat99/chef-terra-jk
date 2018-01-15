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
'''
          }
        }
      }
    }
  }
}