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
		stage("Code analysis reports") {
			steps {
				sh "mvn jacoco:report"
				sh "mvn site"
				publishHTML (target: [
					reportDir: 'target/site/jacoco',
					reportFiles: 'index.html',
					reportName: "JaCoCo Report"
				])
                                publishHTML (target: [
                                        reportDir: 'target/site',
                                        reportFiles: 'checkstyle.html',
                                        reportName: "Checkstyle Report"
                                ])
			}
		}
		stage("code analyses tests") {
			steps {
				sh "mvn verify"
			}
		}		
		stage("Package") {
			steps {
				sh "mvn build"
			}
		}
		stage("Docker build") {
			steps {
				sh "docker build -t mrom42/calculator ."
			}
		}
	}	
}
