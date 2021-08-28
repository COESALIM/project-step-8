node {
  
  stage('Checkout Source Code') {
    checkout scm
  }

  stage('Create Docker Image') {
    docker.build("docker_image:${env.BUILD_NUMBER}")
  }

  stage ('Run Application') {
    try {
      // Stop existing Container
      sh 'docker rm docker_container -f'
      // Start database container here
      sh "docker run -d --name docker_container docker_image:${env.BUILD_NUMBER}"
    } 
	catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
  }
        stage('Deploy our image') { 

            steps { 

                script { 

                    withDockerRegistry(credentialsId: '6aa8b44c-287a-4cd1-8acc-ba7225280288', url: 'https://hub.docker.com/repository/docker/salemalsaadi/my-image-of-project-ubuntu-apache-php') {
					// some block
					} 

                   

                } 
            }
	}
	  stage('Push image') {
    dockerImage.push()
  }
  
 }
