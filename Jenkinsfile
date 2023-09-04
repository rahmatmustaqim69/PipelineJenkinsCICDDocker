pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/rahmatmustaqim69/PipelineJenkinsCICDDocker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t rahmatmustaqim69/webappstest:latest .' 
                sh 'docker tag webappstest rahmatmustaqim69/webappstest:latest'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push rahmatmustaqim69/webappstest:latest'
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 rahmatmustaqim69/webappstest"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://root@192.168.0.117 run -d -p 8003:8080 rahmatmustaqim69/webappstest"
 
            }
        }
    }
	}
    
