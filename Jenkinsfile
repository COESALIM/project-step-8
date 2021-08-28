node {
  
  stage('Checkout Source Code') {
    checkout scm
  }

  stage('Create Docker Image') {
    docker.build("docker_image")
    
   sh "docker tag docker_image  salemalsaadi/test:${env.BUILD_NUMBER}"
  }

  stage ('Run Application') {
    try {
      // Stop existing Container
      sh 'docker rm docker_container -f'
      // Start database container here
      sh "docker run -d --name docker_container  docker_image:${env.BUILD_NUMBER}"
    } 
	catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
  }
  stage ('Push Image'){
  docker.withRegistry('https://registry.hub.docker.com', 'dockerHub') {

  def customImage = docker.build("salemalsaadi/test")

        /* Push the container to the custom Registry */
  customImage.push()
    }
	}

  
 }
