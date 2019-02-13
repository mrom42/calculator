pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
	stages {
		stage("Compile") {
			steps {
				sh "hostname"
				sh "mvn compile"
			}
		}
		stage("Unit test") {
			steps {
				sh "mvn test"
			}
		}
		stage("Code coverage") {
			steps {
				sh "mvn jacoco:report"
				publishHTML (target: [
					reportDir: 'target/site/jacoco',
					reportFiles: 'index.html',
					reportName: "JaCoCo Report"
				])
			}
		}
	}	
}
