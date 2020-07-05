def dockerImageID='sampletest19/phpmysql'
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git branch: 'master',
                url: 'https://github.com/divyarsada/dockerize-phpmysql-app.git'
                sh "ls -lat"
            }
        }
        stage('Lint HTML') {
            steps {
		script {
                    dockerImageID = docker compose.build registry + ":$BUILD_NUMBER"
                    docker-compose up -d
		}
	    }
        }
          
        stage('Upload to AWS') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', docker_cred) {
                    dockerImageID.push()
                    }    
		}
            }
        }
    }
}
