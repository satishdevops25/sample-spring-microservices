pipeline {
agent {
label 'BUILD'
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
       sh "cd /home/ubuntu/workspace/MICROSERVICES/customer-service ; mvn clean install "  
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/MICROSERVICES/customer-service; sudo docker build -t customer-service . "  
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/MICROSERVICES/customer-service ; sudo  docker login -u satishdevops25 -p 9502249024 "
        sh "cd /home/ubuntu/workspace/MICROSERVICES/customer-service ; sudo docker tag 85b9dcac4be6 satishdevops25/customer-service "
        sh "cd /home/ubuntu/workspace/MICROSERVICES/customer-service ; sudo docker push satishdevops25/customer-service  "
        
        
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
