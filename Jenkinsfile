pipeline {
    agent any
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	       

  stage('Docker Build and Tag') {
           steps {
              
                sh 'sudo docker build -t cicd:latest .' 
                sh 'sudo docker tag cicd  pradeepmp1/cicd:latest'
                //sh 'sudo docker tag cicd  pradeepmp1/cicd:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
           	    {
			     steps {
		    withDockerRegistry([ credentialsId:"dockerHub", url: " " ])
				     
			    sh 'docker commit cicd pradeepmp1/cicd:latest'
          sh  'docker push  pradeepmp1/cicd:latest'
        //  sh  'docker push  pradeepmp1/cicd:$BUILD_NUMBER' 
        }
		    }
                  
          
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8000:8090  pradeepmp1/cicd"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@172.31.0.186 run -d -p 8000:8090  pradeepmp1/cicd"
 
            }
        }
    }
	}
    
