pipeline {
  agent any
    stages{
       stage("Build Docker Image"){
           steps{
             sh "docker build -t rohit04445/newapp:${BUILD_ID} ."
          }
       }
       stage("Push Image to Repo"){
          steps{
             sh "docker login -u rohit04445 -p Monty@0045"
             sh "docker push rohit04445/newapp:${BUILD_ID}"
           
          }
       }
 
    }  

}
