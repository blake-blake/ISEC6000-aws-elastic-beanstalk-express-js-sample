pipeline {
    agent {
    	docker { 
		image 'node:16' 
		args '-p 8081:8081' // bind port from app.js in docker to localhost:8081
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
		sh 'cat app.js'
		// npm test
		sh 'snyk test --org=blake-blake --project-name=18821260_Project2_pipeline --severity-threshold=critical'
           
            }
        }
        stage('Deploy') {
            steps {
		sh 'node app.js &'
		sleep 5
		
	
            }
        }
    }
}
