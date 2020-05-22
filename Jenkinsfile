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
          
	 /**
		
	    stage('deploy to cluster') {
		     steps {
			 script {
		            kubernetesDeploy(configs: "frontend.yml" , kubeconfigId: "kube")
		
		        }
		    }
               }
	       **/
	    
	     stage('Deploy to k8s by using kubectl in jenkins') {
	         sh 'kubectl apply -f frontend.yaml'
	       }
	       }
		
	  }
		    
		
		
		
		
		
		      
