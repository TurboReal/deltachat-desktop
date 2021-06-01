pipeline {
    agent any
	
    stages {
        stage('Test') {
            steps {
            	echo 'Testing'
		sh 'npm test'
                
            }
            post{
	    	success{
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Test Succeed',
		    		to: 'nairda98@interia.pl'
	    		
	    	}
		failure{
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Test failed',
		    		to: 'nairda98@interia.pl'
	    	}
	    }
        }
    }
}
