properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git 'https://github.com/boskym/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'  
	}   
	stage('Deploy') {    
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://jenkins-stack-s3bucket-c6h7eunr6qyh/'
	}
	stage('Report') {    
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins-stack'
	}
}
