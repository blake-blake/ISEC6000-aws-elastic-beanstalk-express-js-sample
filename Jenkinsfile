pipeline {
    agent {
    	docker { image 'node:16' } 
    }

    environment {
        SNYK_API_TOKEN = credentials('secret-snyk-api-token')  
    }

	
    stages {
    	stage('Dependency Install') {
	    steps {
	    	sh 'npm install --save' 

		sh 'npm install -g snyk'

		sh 'snyk auth ${SNYK_API_TOKEN}'

		sh 'snyk test --org=blake-blake --project-name=18821260_Project2_pipeline --severity-threshold=critical'
	    }
	}    
        stage('Build') {
            steps {
                echo 'Building..'
                // sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		
                // sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {

		sh 'npm up'
		
		sh 'npm start'
		sh 'sleep 1'
	
            }
        }
    }
}
