pipeline {
  agent any 
    stages {
       stage(‘Unit Test’) {
	    steps {
		git 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
	   }
	  }
	}
 }
