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
            sh 'terraform destroy -force'
          }
        }
        stage('config infra') {
          steps {
            echo 'config infra'
          }
        }
      }
    }
  }
}