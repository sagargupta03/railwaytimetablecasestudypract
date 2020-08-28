//ybmadhu/Configuring-CI-CD-on-Kubernetes-with-Jenkins
pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build -t sagargupt03/railwaytt:${env.BUILD_NUMBER} ."
      }
    }
    stage('Docker Push') {
      steps {
           echo 'Pushing image to Docker Hub....'
        withCredentials([usernamePassword(credentialsId: 'docker_hub_login_SG', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        //  withCredentials([usernamePassword(credentialsId: 'docker_hub_login_SG')]) {
    //      sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
       sh "docker push sagargupt03/railwaytt:${env.BUILD_NUMBER}"
      
            }
          }
      }
    }
}
