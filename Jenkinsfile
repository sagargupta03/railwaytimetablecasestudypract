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
           sh "ping -c 2 ${env.KUBE_MASTER_IP}"
           sh "ping -c 3 localhost"
           sh "cat /proc/sys/net/ipv4/ip_local_port_range" 
        //ketan sir trial 
        //kubernetesDeploy
        //    (
        //            kubeconfigId : 'kubeconfig_cred_sg_ubuntu',
        //            configs : 'railwaytt-simple.yaml',
        //            enableConfigSubstitution: true
        //    )
        
        ////ybmsdhu sir trial 
       //  withKubeConfig([credentialsId: 'kubeconfig_cred_sg_ubuntu']) 
       // {
        //  sh 'cat deployment.yaml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
        //  sh 'kubectl apply -f service.yaml'
        //simpel deployment trial 
        //    sh 'kubectl create -f railwaytt-simple.yaml'
       // }
        
        script {
          kubernetesDeploy(configs: "railwaytt-simple.yaml", kubeconfigId: "kubeconfig_cred_sg_ubuntu" , enableConfigSubstitution: true)
         }
        
            }
          }
    
    
    }
}
