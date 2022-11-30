pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				bat "docker pull abhishekneela/b2b-automation-classplus-store-docker"
			}
		}
		stage("Start Grid"){
			steps{
				bat "docker-compose up -d hub chrome firefox allure allure-ui"
			}
		}
		stage("Run Test"){
			steps{
				bat "docker-compose up TestNG"
			}
		}
		stage('reports') {
    			steps {
    			script {
            			allure([
                    			includeProperties: false,
                    			jdk: '',
                    			properties: [],
                    			reportBuildPolicy: 'ALWAYS',
                    			results: [[path: 'target/allure-results']]
            			])
    			}
    			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			bat "docker-compose down"
		}
	}
}
