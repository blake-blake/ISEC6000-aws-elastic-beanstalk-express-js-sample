pipeline {
    agent {
    	docker { image 'node:16' } 
    }

    stages {
    	stage('Dependency Install') {
	    steps {
	    	sh 'npm install --save' 
	    	snykSecurity organisation: 'Curtin-ISEC6000', projectName: '18821260_Project2_pipeline', severity: 'critical', snykInstallation: 'Please define a Snyk installation in the Jenkins Global Tool Configuration. This task will not run without a Snyk installation.', snykTokenId: 'organisation-snyk-api-token'
	    }
	}    
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'npm run build'
                sh 'npm start'
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh 'kill'
            }
        }
    }
}
