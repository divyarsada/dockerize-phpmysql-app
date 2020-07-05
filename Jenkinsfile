def dockerImageID = 'sampletest19/phpmysql'
pipeline {
  agent any
  stages {
	 stage('Checkout external proj') {
        steps {
            git branch: 'master',
                credentialsId: 'GitHub_key',
                url: 'https://github.com/divyarsada/dockerize-phpmysql-app.git'
            sh "ls -lat"
        }
    }
	stage('Run Docker Compose File')
    {
        dockerImageID = docker-compose.build registry + ":$BUILD_NUMBER"
        sh 'docker-compose up -d'
    }
	stage('Push Image to Docker hub') {
		when {
            branch 'master'
        }
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