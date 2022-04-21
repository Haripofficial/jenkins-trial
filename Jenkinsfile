pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'sudo docker build -t profile-card-image-j:latest .' 
                sh 'sudo docker tag profile-card-image-j haripofficial/profile-card-image-j:latest'
                sh 'sudo docker tag profile-card-image-j haripofficial/profile-card-image-j:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub-hari", url: "" ]) {
          sh  'sudo docker push haripofficial/profile-card-image-j:latest'
          sh  'sudo docker push haripofficial/profile-card-image-j:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "sudo docker run -d -p 4030:80 haripofficial/profile-card-image-j"
 
            }
        }

    }
}
