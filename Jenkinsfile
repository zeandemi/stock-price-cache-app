pipeline {

  environment {
    dockerimagename = "22piston/stock-price-cache-app"
    dockerImage = ""
  }

  agent{
    dockerfile true
  }

  stages {

    stage('Checkout Source') {
      steps {
        echo "Cloning the code"
        git url:'https://github.com/zeandemi/stock-price-cache-app.git', branch: "main"
      }
    }

    stage('Build image') {
      environment{
        
      }
      steps{
        script {
          echo "Building the image"
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'Docker_Cred'
           }
      steps{
        script {
          echo "push to docker hub"  
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push(${BUILD_NUMBER})
          }
        }
      }
    }

  }

}