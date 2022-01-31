pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp ramubobba/samplewebapp:latest'
                //sh 'docker tag samplewebapp ramubobba/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  //stage('Publish image to Docker Hub') {
          
     //       steps {
    //    withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
    //      sh  'docker push ramubobba/samplewebapp:latest'
        //  sh  'docker push ramubobba/samplewebapp:$BUILD_NUMBER' 
   //     }
                  
   //       }
   //     }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -itd -p 8003:8080 ramubobba/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@13.127.35.206 run -d -p 8003:8080 ramubobba/samplewebapp"
 
            }
        }
    }
	}
    
