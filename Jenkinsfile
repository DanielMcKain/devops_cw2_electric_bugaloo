pipeline {
  agent any
  stages {
    stage('Building image'){
      steps{
        script{
          app = docker.build("danielmckain/dm_devops_cw2_r:" + "${env.BUILD_NUMBER}")
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
    stage('Create K8 Deployment'){
      steps{
        script{
          sh "ansible-playbook k8_deploy_docker.YML"
          }
        }
      }
    }
}
