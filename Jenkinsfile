pipeline {
agent {
label 'BUILD'
}

stages 
{
   stage ('Checkout') 
{
steps
    {   
        checkout scm   
    }
    
}
  stage("build & SonarQube analysis") 
{
     steps {
           withSonarQubeEnv('SONARQUBE') 
        {
                sh 'mvn clean package sonar:sonar'
        }
            }
}
   stage("Quality Gate") 
{
       steps 
           {
              timeout(time: 1, unit: 'HOURS') 
              {
                waitForQualityGate abortPipeline: true
              }
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
        sh "cd /home/ubuntu/workspace/MICROSERVICES/customer-service ; sudo docker tag customer-service satishdevops25/customer-service "
        sh "cd /home/ubuntu/workspa1ce/MICROSERVICES/customer-service ; sudo docker push satishdevops25/customer-service  "       
    }
}
   stage('Upload Artifact')
   {
      steps {
        nexusArtifactUploader artifacts: [
           [
                artifactId: 'sample-spring-microservices',
                classifier: '',
                file: target/customer-service.jar,
                type: jar
              ]
        ] ,
           nexusArtifactUploader credentialsId: 'admin', 
           groupId: 'pl.piomin', 
           nexusUrl: '3.111.57.13:8081', 
           nexusVersion: 'nexus2', 
           protocol: 'http', 
           repository: 'http://13.233.91.88:8081/repository/MAVEN', 
           version: '1.0-SNAPSHOT'
            }
   }
stage ('k8sdeployment') 
    {
       steps { 
             sh " sudo ansible-playbook /home/ubuntu/workspace/MICROSERVICES/playbook.yaml"
             }
    }
}  
}
