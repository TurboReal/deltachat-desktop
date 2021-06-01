pipeline {
    agent any
	
    stages {
	    stage('Build') {
		    steps{
		    	echo 'Building'
		    	git url: 'https://github.com/TurboReal/deltachat-desktop'
		    	dir('Docker'){
		    		sh '''
					
					~/docker-compose up -d build-app
				'''
		   	 }
		    }
	    }
            stage('Test') {
            steps {
            	echo 'Testing'
		dir('Docker'){
			sh '~/docker-compose up -d test-app'
		}
                
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
