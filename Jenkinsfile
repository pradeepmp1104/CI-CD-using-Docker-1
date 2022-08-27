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
     
      
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "sudo docker run -d -p 92:92 pradeepmp1/cicd"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                    sh"sudo docker commit cicd  pradeepmp1/cicd:latest"
		    sh"sudo docker push pradeepmp1/cicd:latest"
            }
        }
    }
	}
    
