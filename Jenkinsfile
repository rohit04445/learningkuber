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
             sh "docker login -u rohit04445 -p Monty@04445"
             sh "docker push rohit04445/newapp:${BUILD_ID}"
    
           
          }
       }
       stage("K8s Deployment"){
          steps{
             sh "chmod +x myscript.sh"
             sh " sh myscript.sh ${BUILD_ID}" 
             sshagent(['ubuntu']) {
                 sh "scp -o StrictHostKeyChecking=no  newdep.yaml ubuntu@3.110.117.118:/home/ubuntu"
                 script{
                   try{
                      sh "ssh ubuntu@3.110.117.118 kubectl create -f newdep.yaml"
                   }
                   catch(error){
                        sh "ssh ubuntu@3.110.117.118 kubectl apply -f newdep.yaml"
                   }
                
                 }
             }           
            
          }
       }
 
    }  

}
