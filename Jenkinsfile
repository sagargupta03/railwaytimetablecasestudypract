//ybmadhu/Configuring-CI-CD-on-Kubernetes-with-Jenkins
pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
       // sh "docker build -t sagargupta03/railwaytt:${env.BUILD_NUMBER} ."
         sh "docker build -t sagargupta03/railwaytt ."
      }
    }
    stage('Docker Push') {
      steps {
           echo 'Pushing image to Docker Hub....'
        withCredentials([usernamePassword(credentialsId: 'docker_hub_login_SG', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        //  withCredentials([usernamePassword(credentialsId: 'docker_hub_login_SG')]) {
          sh "echo ${env.dockerHubUser}"
          sh "echo ${env.dockerHubPassword}"
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          //  sh "docker push sagargupta03/railwaytt:${env.BUILD_NUMBER}"
            sh "docker push sagargupta03/railwaytt"
      
            }
          }
      }
     stage('K8 initiate') {
      steps {
           sh "echo ${env.KUBE_MASTER_IP}"
        //   withKubeConfig([credentialsId: 'kubeconfig_cred_SG']) {
        // sh 'cat sample.yml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
          //sh 'kubectl apply -f service.yaml'
           kubernetesDeploy(
                    kubeconfigId: 'kubeconfig_cred_SG',
                    //configs: 'railwaytt-kube-canary.yml',
                    configs:  railwaytt-kube.yml,
                    //configs: 'railwaytt-kube-SG.yml',
                    enableConfigSubstitution: true
                    
                )
       // }
            }
          }
    
    
    }
}
