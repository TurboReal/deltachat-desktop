pipeline {
    agent any
	
    stages {
	    stage('Build') {
		    steps{
		    	echo 'Building'
		    	git url: 'https://github.com/TurboReal/deltachat-desktop'
		    	dir('Docker'){
		    		sh '''
					ls
					curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o ~/docker-compose
					chmod +x ~/docker-compose
					~/docker-compose up
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
