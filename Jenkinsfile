properties([pipelineTriggers([githubPush()])])


node('linux'){

         stage(‘Unit Test’) {
	    
		git credentialsId: 'github-credential', url: 'https://github.com/gesusu/java-project.git'
		 sh 'ant -f test.xml -v'
	}
	 
	stage (‘Build’) {
	   
		sh 'ant -f build.xml -v'
	 
	} 
	stage (‘Deploy’) {
	   
		echo "Copying to s3 bucket gbjenkins.com"
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://gbjenkins.com/jenkinsdist'
      
	}
        stage (‘Report’) {
	   
	      echo "Generating a report of the CloudFormation stack resources of the environment"
	      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                  sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        
       }
   }
 }
