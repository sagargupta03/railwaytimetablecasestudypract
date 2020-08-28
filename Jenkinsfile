pipeline 
{
    agent any
        environment
            {
        //be sure to replace "ketanvj" with your own Docker Hub username
                  DOCKER_IMAGE_NAME = "ketanvj/railwaytt"
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
                when {
                branch 'master'
                     }
                steps {
                  script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    app.inside {
                        sh 'echo Hello, World!'
                               }
                         }
                      }
            }
            stage('Push Docker Image')
            {
                 when {
                  branch 'master'
                      }
                 steps {
                   script {
                     docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_login')
                         {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                          }
             }
        }
      }
}
