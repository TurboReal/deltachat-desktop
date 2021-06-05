pipeline {
    agent any
	
    stages {
	    stage('Build') {
		    steps{
		    	echo 'Building'
		    	git credentialsId: 'git_credentials', url: 'https://github.com/TurboReal/deltachat-desktop'
		    	dir('Docker'){
		    		sh '''
					ls -l
					docker --version
					curl -L "https://github.com/docker/compose/releases/download/1.29.0/docker-compose-$(uname -s)-$(uname -m)" -o ~/docker-compose
					ls -l ~/docker-compose
					chmod +x ~/docker-compose
					ls -l ~/docker-compose
					docker-compose --version
					~/docker-compose up build-app
				'''
		   	 }
		    }
	    }
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
