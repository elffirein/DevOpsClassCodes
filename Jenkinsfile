
pipeline{
    tools{
        jdk 'myJDK'
        maven 'mymaven'
    }
	agent any
      stages{
           stage('Checkout'){
	    	 environment {
                        SERVICE_CREDS = credentials('jenkins-example-github-pat')
               }
               steps{
		 echo 'cloning1..'
                 git credentialsId: 'jenkins-example-github-pat', url: 'https://github.com/Sonal0409/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
             
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
		  
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		  
              steps{
	         echo 'Testing'
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
           stage('MetricCheck'){
              
              steps{
                  sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
              }
              
          }
          stage('Package'){
		  
              steps{
		  
                  sh 'mvn package'
              }
          }
	     
          
      }
}
