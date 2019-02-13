pipeline {
	agent any
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
	}	
}
