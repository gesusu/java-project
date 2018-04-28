pipeline {
  agent any 
    stages {
       stage(‘Test’) {
	    steps {
		git 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
	   }
	  }
     }
 }
