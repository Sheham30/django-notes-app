pipeline {
	agent any

	stages {
    	stage("Code"){
    		steps {
    	        echo "Cloning the code"
    	        git url:"https://github.com/Sheham30/django-notes-app", branch:"main"
            }
        }
	
    	stage("Build"){
    		steps {
    	        echo "Building the code"
    	        sh "docker build -t my-note-app ."
            }
        }
    
    	stage("Push to Docker Hub"){
    		steps {
    	        echo "Push the image to docker hub"
    	       // Logging into dockerhub using environment variable
    	        withCredentials([usernamePassword(credentialsId:"dockerhubcreds", passwordVariable:"dockerhubPass", usernameVariable:"dockerhubUser")]) {
    	            sh "docker tag my-note-app ${env.dockerhubUser}/my-note-app:latest"
    	            sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
    	            sh "docker push ${env.dockerhubUser}/my-note-app:latest"
    	        }
            }
        }   
    
    	stage("Deploy"){
    		steps {
    	        echo "Deploying the container"
    	        sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
