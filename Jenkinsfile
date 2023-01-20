pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="252316791856"
        AWS_DEFAULT_REGION="us-east-1"
        IMAGE_REPO_NAME="test/team4"
        IMAGE_TAG="v1"
        REPOSITORY_URI = "252316791856.dkr.ecr.us-east-1.amazonaws.com/test/team4"
    }
	
	  tools
    {
       maven "maven"
    }
 stages {
      //stage('Logging into AWS ECR') {
         // steps {
                //script {
                //sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 252316791856.dkr.ecr.us-east-1.amazonaws.com"
               // }
                 
           // }
       // }	 
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Big-Zaza/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  /*stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push nikhilnidhi/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
       } 
       */
	// Uploading Docker images into AWS ECR
  /*  stage('Pushing to ECR') {
     steps{  
         script {
            //    sh """docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URI}:$IMAGE_TAG"""
		  sh """docker tag test/team4:latest 252316791856.dkr.ecr.us-east-1.amazonaws.com/test/team4:latest"""
		  sh """docker push 252316791856.dkr.ecr.us-east-1.amazonaws.com/test/team4:latest"""
              //  sh """docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"""
         }
        }
      }
      */
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8021:8080 nikhilnidhi/samplewebapp"
 
            }
        }
 /*
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
            }
        }
	*/
    }
	}

    
