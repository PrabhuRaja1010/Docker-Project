pipeline {

    agent any
    stages {
	stage('Checkout Source') {
           steps {
             git 'https://github.com/PrabhuRaja1010/Docker-Project.git'
          }
		
	}
		
		stage('build image') {
		  steps {
		     script {
	               sampleapp = docker.build("prabhuraja/hello:${env.BUILD_ID}")
		        }
		    }
		}
        stage("push image") {
           steps {
             script { 
	         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                      sampleapp.push("latest")
                      sampleapp.push("${env.BUILD_ID}")
                    }
                }
            }
	}					
                   			 
		
	    stage("deploy to k8s"){
		    kubernetesDeploy{
                        configs: " frondend.yaml " ,
                        kubeconfigId: " kube " ,
                        enableConfigSubstitution: true
		        }
		    }
              
		
	       }	
		
	  }
		
		
		
		
		
		
		
		      
