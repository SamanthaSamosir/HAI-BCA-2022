node{
  def dockerImageName='samanthams/htmltest_$JOB_NAME:$currentBuild'
  def dockerContainerName='simplehtml_$currentBuild'
  def dockerPrevName='simplehtml_$previousBuild'
  
  stage('SCM Checkout'){
    git 'https://github.com/SamanthaMeliora/HTMLtest.git'
  }
  
  stage('Stop Active Container'){
    sh "docker stop ${dockerPrevName}"
  }
  
  stage('Build Docker Image'){
    sh "docker build -t ${dockerImageName} ."
  }
  
  stage('Run Docker Image'){
      sh "docker run -p 8082:8080 -d --name ${dockerContainerName} ${dockerImageName}"
      }  
}
