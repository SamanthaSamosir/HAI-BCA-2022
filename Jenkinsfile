node{
		
	options{
		timeout(time: 7, unit: "MINUTES")
		}
	def dockerImageName='test:$BUILD_NUMBER'
  	def dockerContainerName='simplehtml_$BUILD_NUMBER'
  	withCredentials(
		([string(credentialsId: 'telegramToken', variable: 'TOKEN'),
		string(credentialsId: 'telegramChatId', variable: 'CHAT_ID')])) {
			sh 'curl -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d "chat_id=${CHAT_ID}" -d text="Jenkins start deploy"'
  		}
  
	stage('SCM'){
		try {
			echo 'checkout from git'
			git url: 'https://github.com/SamanthaMeliora/HTMLtest.git', branch: 'master'
		} catch(err) {
	        	throw err
      		}
  	}
 
	stage('Deploy'){
		
		try {
			sh "docker build -t ${dockerImageName} ."
			sh "docker run -itd --name ${dockerContainerName} -p 80 ${dockerImageName}"
		} catch (err) {
			echo err.getMessage()
        		withCredentials(
				([string(credentialsId: 'telegramToken', variable: 'TOKEN'),
      				string(credentialsId: 'telegramChatId', variable: 'CHAT_ID')])) {
        				sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d "chat_id=${CHAT_ID}"  -d text="[❌] Failed to build 😱"'
        				sh 'exit 1'
				}     
	  	}   
	  	withCredentials(
			([string(credentialsId: 'telegramToken', variable: 'TOKEN'),
      			string(credentialsId: 'telegramChatId', variable: 'CHAT_ID')])) {
      				sh 'curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d "chat_id=${CHAT_ID}"  -d text="[✅] Build successfully 😊"'
  			} 
  	}
}
