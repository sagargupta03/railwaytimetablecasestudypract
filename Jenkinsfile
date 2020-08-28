pipeline 
{
    agent any
        environment
            {
        //be sure to replace "ketanvj" with your own Docker Hub username
                 // DOCKER_IMAGE_NAME = "sagargupta03/railwaytt"
                //DOCKER_IMAGE_NAME = "ketanvj/railwaytt"
                 registry = "sagargupta03/railwaytt"
                registryCredential = 'docker_hub_login_SG'
            }
        stages
        {
            stage('Build')
            {
              steps
                {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/railwaytt.zip'
                 }
            }
            stage('Build Docker Image')
            {
                //when {
                //branch 'master'
                  //   }
                 
                steps {
                    echo 'Build Docker image'
                  script {
                   // app = docker.build(DOCKER_IMAGE_NAME)
                      docker.build registry + ":$BUILD_NUMBER"
                    app.inside {
                        sh 'echo docker build'
                               }
                         }
                      }
            }
            stage('Push Docker Image')
            {
                 //when {
                  //branch 'master'
                    //  }
                 steps {
                   script {
                     docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login_SG')
                         {
                              sh 'echo docker push'
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                          }
             }
        }
      }
   }
}
