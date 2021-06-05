pipeline {
    agent any
	
    stages {
	    
            stage('Test') {
            steps {
            	echo 'Testing'
		dir('Docker'){
			sh '~/docker-compose up test-app'
		}
                
            }
            post{
	    	success{
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [[$class: 'DevelopersRecipientProvider']],
		    		subject: 'Test Succeed',
		    		to: 'turboreal9812@gmail.com'
	    		
	    	}
		failure{
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Test failed',
		    		to: 'turboreal9812@gmail.com'
	    	}
	    }
        }
    }
}
