pipeline{
  agent any
  environment{
    DOCKERHUB_REPO='docker.io'
    USER='mulyonoaja'
    PASS='dckr_pat_1NSUpPR74PXY6MljFSoXt-L-Jvo'
    
  }
  stages{
    stage("build image"){
      steps{
        sh "docker --version"
        sh "docker build -t mulyonoaja/vbox:test1" 
        echo "image built successfully"
      }     
    }
    stage("push image to Dockerhub"){
      steps{
        echo "pushing to dockerhub stage"
        withCredentials([usernamePassword(credentialsId: '5b3bfd70-ae02-49d2-984e-6f98a520f000', passwordVariable: 'PASS', usernameVariable: 'USER')]){
          sh "echo $PASS | docker login $DOCKERHUB_REPO --username $USER --password-stdin"
          sh "nslookup docker.io"
          sh "docker push mulyonoaja/vbox:test1"
        }
        echo "image pushed successfully to azure container registry"
      }
    }
  }
}
