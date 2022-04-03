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
        sh "cd /home/ubuntu/workspace/jenkins-piplinejob/customer-service; sudo docker build -t customer-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/customer-service ; sudo  docker login -u nagurbabu -p @Nagur336 "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/customer-service ; sudo docker tag account-service nagurbabu/customer-service "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/customer-service ; sudo docker push nagurbabu/customer-service  "
        
        
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
