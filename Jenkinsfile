pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000'
	}
    }
    environment {
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
		sh 'npm config set registry https://registry.npm.taobao.org'
		sh 'npm install'
		// sh 'npm install webpack-dev-server -g --registry=https://registry.npm.taobao.org'
                // sh 'npm install --registry=https://registry.npm.taobao.org'
		    
		   
            }
        }
        stage('Test'){
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
		input message:  'Finished using the web site? (Click "Proceed" to continue)'
		sh './jenkins/scripts/kill.sh'
	    }
        }
    }
}
