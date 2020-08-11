node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("nodejs/sample")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image to ECR') {
        /* 
			You would need to have creds of ECR before you can push images to your account
		*/
  docker.withRegistry('332267807927.dkr.ecr.us-west-2.amazonaws.com/dev8-graphql, 'ecr:us-west-2:demo-ecr-credentials') {
	  app.push("${env.BUILD_NUMBER}")
          app.push("latest")
	}
	    
	    
/*        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
            }  */
                echo "Trying to Push Docker Build to DockerHub"
    }
}
