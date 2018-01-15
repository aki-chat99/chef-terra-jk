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
terraform output pub_ip>>a.txt
cp -f /var/lib/jenkins/test2/a.txt /var/lib/jenkins/test2/chef
rm -f /var/lib/jenkins/test2/a.txt
rm -f /var/lib/jenkins/test2/variables.tf'''
          }
        }
        stage('config infra') {
          steps {
            echo 'config infra'
            sh '''cd /var/lib/jenkins/test2/chef

old_IFS=$IFS
IFS=$\',\'
lines=($(cat a.txt)) # array
IFS=$old_IFS
a=$( wc -l <a.txt)
max=$a
for ((c=0; c<max; c++ ))
do
x=( $(echo ${lines[c]}))
echo $x
b=node
z=$((z +001))
node=$b$z
echo $node
knife bootstrap $x -N $node -i /home/ec2-user/chef-repo/.chef/ankit_565881_ohio.pem -x ec2-user --sudo -r recipe[apache] -y
sleep 30
done
rm /var/lib/jenkins/test2/chef/a.txt'''
          }
        }
      }
    }
  }
}