properties([pipelineTriggers([githubPush()])])


pipeline {   
  agent any 
    stages {
       stage(‘Test’) {
	    steps {
		git credentialsId: 'github-credential', url: 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
		
	   }
	  }

    }
 }

