node{
  def dockerImageName='htmltest:$BUILD_NUMBER'
  def dockerContainerName='simplehtml_$BUILD_NUMBER'
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
    def dockerRun ='docker run -p 8082:80 -d --name ${dockerContainerName} ${dockerImageName}'
    sshagent(['400939f3-d17a-43c3-8e2e-7cc98bdb1253']) {
      sh 'ssh -tt StrictHostKeyChecking=no root@172.31.15.226 ${dockerRun}'
    }
  }  
}
