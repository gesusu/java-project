properties([pipelineTriggers([githubPush()])])


pipeline {   
  agent {
     node{
       label'linux'
    }
  }
    stages {
       stage(‘Test’) {
	    steps {
		git credentialsId: 'github-credential', url: 'https://github.com/gesusu/java-project.git'
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

