pipeline {
	agent any 
	stages {
       stage(‘Unit Test’) {
	    steps {
		git '
		sh 'ant -f test.xml -v'
	   }
	  }
	}
 }
