pipeline{
  agent any
  environment{
    AZURE_REPO='myprivaterepo.azurecr.io'
  }
  stages{
    stage("build image"){
      steps{
        sh "docker build -t myprivaterepo.azurecr.io/library-management-api ./api/" 
        echo "image built successfully"
      }     
    }
    stage("push image to ACR"){
      steps{
        echo "pushing to ACR stage"
        withCredentials([usernamePassword(credentialsId: 'azure-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]){
          sh "echo $PASS | docker login ${AZURE_REPO} --username $USER --password-stdin"
          sh "nslookup myprivaterepo.azurecr.io"
          sh "docker push myprivaterepo.azurecr.io/library-management-api"
        }
        echo "image pushed successfully to azure container registry"
      }
    }
  }
}
