node{
  def dockerImageName='htmltest:$BUILD_NUMBER'
  def dockerContainerName='simplehtml_$BUILD_NUMBER'
  //def dockerPreviousContainer='simplehtml_$51'
  
  //def dockerPrevImage=''
  
  stage('SCM'){
    //pull from this repo bitj
    git 'https://github.com/SamanthaMeliora/HTMLtest.git'
  }
  
 // stage('Pull the newest Image'){
   // sh ""
   //}
  
  stage('Build Docker Image'){
    sh "docker build -t ${dockerImageName} ."
  }
  
  stage('Run Container'){
    //sh "docker stop ${dockerPreviousContainer}"
    sh "docker run -p 8082:80 -d --name ${dockerContainerName} ${dockerImageName}"
  }
}

  //sshagent(['dev-server']) {
      //sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.15.226 ${dockerRun}'
    //}
  //} 
