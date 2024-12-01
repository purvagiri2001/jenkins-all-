pipeline{
   agent any

   environment{
     GIT_REPOSITORY_URL = "https://github.com/purvagiri2001/jenkins-all-.git"
     DOCKER_IMAGE_NAME = 'purvagiri2001/docker_jenkins_demo'
     IMAGE_TAG = '1.0'
   }


   stages{
     stage('Clone Repository'){
       steps{
         script{
           try{
              git branch:'main', url:GIT_REPOSITORY_URL
           }catch(Exception e){
               echo "Failed to clone repository:${e.message}"
               error "Failed to clone repository"
      }
   }
  }
}
