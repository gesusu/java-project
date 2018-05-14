properties([pipelineTriggers([githubPush()])])


node('linux'){

    stage(‘Test’) {
	    step {
		git credentialsId: 'github-credential', url: 'https://github.com/gesusu/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
		}
    }
	stage (‘Build’) {
	    step {
		sh 'ant -f build.xml -v'
	  }
	} 
	stage (‘Deploy’) {
	    step {
		echo "Copying to s3 bucket gbjenkins.com"
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://gbjenkins.com/jenkinsdist'
           }
	}
        stage (‘Report’) {
	    step {
	      echo "Generating a report of the CloudFormation stack resources of the environment"
	      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                  sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }
       }
   }
 }
