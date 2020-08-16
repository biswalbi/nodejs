agentName = "ubuntu-1"
pipeline {
    agent none
	
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
	    agentName="ubuntu-1"
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("biswalbi/test")
	    agentName="ubuntu-1"
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
		agentName="ubuntu-1"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
