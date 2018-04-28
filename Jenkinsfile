pipeline {
  agent any 
    stages {
       stage(‘Test’) {
	    steps {
		git 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
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
			// withAWS step provides authorization for the nested steps
                              s3Upload(file:'rectangle-3.jar', bucket:'gbjenkins.com', path:'var/jenkins_home/workspace/java-pipeline/dist/rectangle-3.jar')	
	   }
	}
	stage (‘Report’) {
	   steps {
		   
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '14dd1bff-3295-4649-a919-3fc6ad57f627', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {    
		     sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
	 }
       }
     }
 }
