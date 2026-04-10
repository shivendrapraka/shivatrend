pipeline {
  agent any
  environment {
    PATH = "/opt/maven/bin:$PATH"
   }
  stages {
    stage ("build") {
       steps {
          sh "mvn clean deploy"
       }
	}
    stage ("SonarQube analysis") {
	   environment {
	       ScannerHome = tool 'sonarqube_scanner'
		}
	   steps {
	     withSonarQubeEnv ('shiva-sonarqube-server') {
		 sh "${ScannerHome}/bin/sonar-scanner"
		 }
	   }
    }
  }
}
