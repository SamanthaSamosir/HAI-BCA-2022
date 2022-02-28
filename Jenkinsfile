node{
  def dockerImageName='samanthams/htmltest_$JOB_NAME:$BUILD_NUMBER'
  stage('SCM Checkout'){
    git 'https://github.com/SamanthaMeliora/HTMLtest.git'
  }
  stage('Build Docker Image'){
    sh "docker build -t ${dockerImageName} ."
  }
  
  stage('Publish Docker Image'){
    withCredentials([string(credentialsID: 'dockerpwd', variable: 'dockerPWD')]){
      sh "docker login -u samanthams -p ${dockerPWD}"
    }
    sh "docker push ${dockerImageName}"
  }
  stage('Run Docker Image'){
    def dockerContainerName = 'htmltest_$JOB_NAME_$BUILD_NUMBER'
    def dockerRun = "sudo docker run -p 8082:8080 -d --name ${dockerContainerName} ${dockerImageName}"
    withCredentials([string(credentialsId: 'deploymentserverpwd', variable: 'dpPWD')]){
      sh "sshpass -p ${dpPWD} ssh -o StrictHostKeyChecking=no root@108.136.232.253"
      sh "sshpass -p ${dpPWD} scp -o StrictHostKeyChecking=no root@108.136.232.253 ${dockerRun}"
    }
  }  
}
