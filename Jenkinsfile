pipeline {
    agent any
	
    stages {
        stage('Test') {
            steps {
            	echo 'Testing'
                sh 'npm install'
		sh 'npm test'
                
            }
            post{
	    	success{
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Test Succeed',
		    		to: 'nairda6666@gmail.com'
	    		
	    	}
		failure{
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Test failed',
		    		to: 'nairda6666@gmail.com'
	    	}
	    }
        }
    }
}
