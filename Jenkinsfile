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
          // THIS IS A COMMENT sh "ansible-playbook k8_deploy_docker.YML"
          sh "ssh -i \"/home/devops_cw2_electric_bugaloo/DevOps_Cw2.pem\" ubuntu@54.82.135.136 'ansible-playbook /home/ubuntu/devops_cw2_electric_bugaloo/k8_deploy_docker.YML'"
          }
        script{
          sh "ssh -i \"/home/devops_cw2_electric_bugaloo/DevOps_Cw2.pem\" ubuntu@54.82.135.136 'ansible-playbook /home/ubuntu/devops_cw2_electric_bugaloo/k8_scale.YML'"
          }
        }
      }
    }
}