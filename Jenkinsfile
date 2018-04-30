properties([pipelineTriggers([githubPush()])])


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
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://gbjenkins.com/Assignment10/'
          }
	}
    }
 }

