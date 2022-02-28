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
  
  stage('Run Docker Image'){
      //sh "systemctl enable nginx"
      sh "docker run -p 8082:8080 -d --name ${dockerContainerName} ${dockerImageName}"
      }  
}
