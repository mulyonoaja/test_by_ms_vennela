pipeline{
  agent any
  environment{
    DOCKERHUB_REPO='docker.io'
  }
  stages{
    stage("build image"){
      steps{
        sh "docker build -t mulyonoaja/vbox:test1" 
        echo "image built successfully"
      }     
    }
    stage("push image to Dockerhub"){
      steps{
        echo "pushing to ACR stage"
        withCredentials([usernamePassword(credentialsId: 'azure-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]){
          sh "echo $PASS | docker login ${DOCKERHUB_REPO} --username $USER --password-stdin"
          sh "nslookup myprivaterepo.azurecr.io"
          sh "docker push myprivaterepo.azurecr.io/library-management-api"
        }
        echo "image pushed successfully to azure container registry"
      }
    }
  }
}
