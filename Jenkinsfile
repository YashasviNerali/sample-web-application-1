
   


node{        
        stages{


		stage('sonarstage'){
                  steps{
                      script{
                      withSonarQubeEnv('sonar') { 
                      sh "mvn sonar:sonar"
                       }
                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
		    sh "mvn clean install"
                  }
		  }       }  
              }



              stage('build')
                {
              steps{
                  script{
		# sh 'cp -r ../devops-training@2/target .'
                   sh 'docker build . -t yashasvinerali/app1:1.0.0'
		   withCredentials([string(credentialsId: 'docker_password', variable: 'docker_password')]) {
				    
				  sh 'docker login -u yashasvinerali -p $docker_password'
				  sh 'docker push yashasvinerali/app1:1.0.0
			}
                       }
                    }
                 }
		 
		
	       
	       
	       
	      
    
}
