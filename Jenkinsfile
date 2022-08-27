pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/pradeepmp1104/CI-CD-using-Docker-1.git'
             
          }
        }
	

  stage('Docker Build and Tag') {
           steps {
                sh 'sudo docker build -t cicd:latest .' 
                sh 'sudo docker tag cicd pradeepmp1/cicd:latest'
                		             sh  'sudo docker push pradeepmp1/cicd:latest'
                                 //sh 'docker tag cicd pradeepmp1/cicd:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "https://hub.docker.com/" ]) 
		    {
          //sh  'sudo docker push pradeepmp1/cicd:latest'
        //  sh  'docker push pradeepmp1/cicd:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "sudo docker run -d -p 8000:8090 pradeepmp1/cicd"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "sudo docker -H ssh://jenkins@172.31.0.186 run -d -p 8000:8090 pradeepmp1/cicd:latest"
 
            }
        }
    }
	}
    
