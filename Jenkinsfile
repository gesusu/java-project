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
	      stage (‘Deploy’) {
	   steps {
		echo "Copying to s3 bucket gbjenkins.com"
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    s3Upload(file:'rectangle-2.jar', bucket:'gbjenkins', path:'/workspace/java-pipeline/dist/rectangle-2.jar')
        }
	   }
		
     }
    }
 }

