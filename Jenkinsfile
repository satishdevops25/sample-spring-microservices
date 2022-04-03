pipeline {
agent {
label 'buildserver'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/customer-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/jenkins-piplinejob/account-service; sudo docker build -t customer-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo  docker login -nagurbabu -@Nagur336 "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker tag account-service nagurbabu/customer-service "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker push nagurbabu/account-service  "
        
        
    }
}
 
   
stage ('k8sdeployment') 
    {
       steps {
           node (' ansible') {
             sh " sudo ansible-playbook /etc/ansible/k8s.yaml"
   
    }
}
}
}
    
    
}
