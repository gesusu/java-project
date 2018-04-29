properties([pipelineTriggers([githubPush()])])


pipeline {   
  agent any 
    stages {
       stage(‘Test’) {
	       echo "Copying to s3 bucket gbjenkins.com"
	    steps {
		
		git credentialsId: 'github-credential', url: 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/*.xml'
	   }
	  }
	stage (‘Build’) {
	   steps {
		sh 'ant -f build.xml -v'
	 }
	} 
	stage (‘Deploy’) {
	   steps {
		echo "Copying to s3 bucket gbjenkins.com"
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://gbjenkins.com/jenkinsdist'
          }
	}
        stage (‘Report’) {
	   steps {
	      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                  sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
             }
	}
      }
    }
 }

