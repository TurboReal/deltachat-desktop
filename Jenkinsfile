pipeline {
    agent any
	
	tools{nodejs "nodejs"}
	
    stages {
        stage('Test') {
            steps {
            	echo 'Testing'
                sh '~/docker-compose up -d test-app'
                
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
