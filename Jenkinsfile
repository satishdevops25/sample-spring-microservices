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
       sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/jenkins-piplinejob/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo  docker login -nagurbabu -@Nagur336 "
        sh "cd /home/ubuntu/workspace/jenkins-pipelinejob/account-service ; sudo docker tag account-service nagurbabu/account-service "
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
