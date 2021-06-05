pipeline {
    agent any
	
    stages {
	    stage('Build') {
		    steps{
		    	echo 'Building'
		    	git url: 'https://github.com/TurboReal/deltachat-desktop'
		    	dir('Docker'){
		    		sh '''
					ls -l
					curl -L "https://github.com/docker/compose/releases/download/1.29.0/docker-compose-$(uname -s)-$(uname -m)" -o ~/docker-compose
					chmod +x ~/docker-compose
					docker-compose --version
					~/docker-compose up --build build-app
				'''
		   	 }
		    }
		    post{
	    		success{
				echo 'Building - success'
	    			emailext attachLog: true,
		    			body: "Status: ${currentBuild.currentResult}",
		    			recipientProviders: [[$class: 'DevelopersRecipientProvider']],
		    			subject: 'Test Succeed',
		    			to: 'turboreal9812@gmail.com'
	    		
	    		}
			failure{
				echo 'Building- failure'
				emailext attachLog: true,
					body: "Status: ${currentBuild.currentResult}",
					recipientProviders: [developers()],
					subject: 'Test failed',
					to: 'turboreal9812@gmail.com'
	    		}
	    }
	    }
            stage('Test') {
		    when{ expression{currentBuild.result == 'SUCCESS' || currentBuild.result == null}}
            steps {
            	echo 'Testing'
		git url: 'https://github.com/TurboReal/deltachat-desktop'
		dir('Docker'){
			sh '~/docker-compose up --build test-app'
		}
                
            }
            post{
	    	success{
			echo 'Testing - success'
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [[$class: 'DevelopersRecipientProvider']],
		    		subject: 'Test Succeed',
		    		to: 'turboreal9812@gmail.com'
	    		
	    	}
		failure{
			echo 'Testing - failure'
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Test failed',
		    		to: 'turboreal9812@gmail.com'
	    	}
	    }
        }
	    stage('Deploy') {
		    steps{
		    	echo 'Deploying'
		    	git url: 'https://github.com/TurboReal/deltachat-desktop'
		    }
		    post{
	    		success{
				echo 'Deploying - success'
	    			emailext attachLog: true,
		    			body: "Status: ${currentBuild.currentResult}",
		    			recipientProviders: [[$class: 'DevelopersRecipientProvider']],
		    			subject: 'Deploy Succeed',
		    			to: 'turboreal9812@gmail.com'
	    		
	    		}
			failure{
				echo 'Deploying- failure'
				emailext attachLog: true,
					body: "Status: ${currentBuild.currentResult}",
					recipientProviders: [developers()],
					subject: 'Deploy failed',
					to: 'turboreal9812@gmail.com'
	    		}
	    }
	    }
    }
	post{
	    	success{
			echo 'Success'
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [[$class: 'DevelopersRecipientProvider']],
		    		subject: 'Succeed',
		    		to: 'turboreal9812@gmail.com'
	    		
	    	}
		failure{
			echo 'Failure'
	    		emailext attachLog: true,
		    		body: "Status: ${currentBuild.currentResult}",
		    		recipientProviders: [developers()],
		    		subject: 'Failed',
		    		to: 'turboreal9812@gmail.com'
	    	}
	    }
}
