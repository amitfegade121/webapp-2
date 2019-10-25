pipeline {

	agent any
	
	stages {
		
		stage('Build') {
			steps {
				bat label: '', script: 'mvn clean package'
			}
			post {
				success {
					echo 'Archiving the artifact....'
					archiveArtifacts '**/*.war'
				}
				failure {
				echo 'Failed to archive...'
				}
			}
		}
		

		stage('Deploy to staging environment') {
			steps {
				deploy adapters: [tomcat9(credentialsId: 'ce671af0-748c-431d-beb8-294eeb06c7f8', path: '', url: 'http://localhost:8211')], contextPath: null, war: '**/*.war'
			}
			post {
				success {
					echo 'Application is deployed to staging environment successfully...'
				}
				failure {
					echo 'Failed to deploy an application...'
				}
			}
		}
	}
}







