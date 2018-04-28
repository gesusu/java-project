properties([pipelineTriggers([githubPush()])])


pipeline {   
  agent any 
    stages {
       stage(‘Test’) {
	    steps {
		git 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/*.xml'
	   }
	  }
	stage (‘Build’) {
	   steps {
		sh 'ant -f build.xml -v'
	 }
	} 
	stage (‘Report’) {
	   steps {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                  sh 'AWS cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
             }
	}
	}	
    }
 }

