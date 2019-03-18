pipeline {
    agent  { label 'master' }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                
            }
        }
        stage('DeployToStaging') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("prashkotak/build-test")
                   
                }
			}				
        }
		stage('DockerPush') {
			when {
                branch 'master'
            }
			steps {
				script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
				}
			} 	   		
		}
        
    }
}