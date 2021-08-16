pipeline {
  agent any

  stages {
    stage('Building image'){
      steps{
        script{
          app = docker.build("danielmckain/dm_devops_cw2_r")
        }
      }
    }

    stage('Pushing Image'){
      steps{
        script{
          docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials'){
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
          }
        }
      }
    }

    stage('Roll Update'){
      steps{
          //Your code goes here
      }
    }

  }

}
