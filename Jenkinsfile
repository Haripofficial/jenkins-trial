pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t profile-card-image-j:latest .' 
                sh 'docker tag profile-card-image-j haripofficial/profile-card-image-j:latest'
                sh 'docker tag profile-card-image-j haripofficial/profile-card-image-j:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub-hari", url: "" ]) {
          sh  'docker push haripofficial/profile-card-image-j:latest'
          sh  'docker push haripofficial/profile-card-image-j:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 4030:80 haripofficial/profile-card-image-j"
 
            }
        }

    }
}
