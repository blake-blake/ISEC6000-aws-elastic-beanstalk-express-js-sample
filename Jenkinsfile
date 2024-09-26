pipeline {
    agent {
    	docker { 
		image 'node:16' 
		args '-p 8081:8081'
	} 
    }

    environment {
        SNYK_API_TOKEN = credentials('secret-snyk-api-token')  
    }

	
    stages {
    	stage('Dependency Install') {
	    steps {
	    	sh '''
      			npm install --save
		    	npm install -g snyk
		    	snyk auth ${SNYK_API_TOKEN}
		    	snyk test --org=blake-blake --project-name=18821260_Project2_pipeline --severity-threshold=critical
       		'''
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
		sh 'node app.js'
		//sh 'npm up'
		//sh 'npm start'
		//sh 'sleep 1'
	
            }
        }
    }
}
