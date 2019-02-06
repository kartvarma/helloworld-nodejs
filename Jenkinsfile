pipeline {
    agent any
    
    tools  {
           maven 'maven3.6.0'
           jdk 'java1.8.0'
           }
           
    stages {
	 
    	 stage('Build') {
    	    steps {
    		    echo 'Running build Automation' 
            sh "mvn -B -DskipTests clean package"
    	       }		
    	    }

    	stage ('Build Docker Image') {
    		steps {
    		   script {
    			app=docker.build("kartvarma/node-app")
    			app.inside {
    				sh 'echo $(curl http://54.244.72.37:8080)'
    			 	}
    	       		}
    	    	 }
    	}
    	
    	stage('Push Docker Image') {
    		steps {
    		  script {
    			docker.withRegistry('https://registry.hub.docker.com','dockhub') {
    			app.push("latest")
    			}
    		  }
            }
    	}    
   }
}
