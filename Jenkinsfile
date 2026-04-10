pipeline {
  agent any
  environment {
    PATH = "/opt/maven/bin:$PATH"
   }
  stages {
    stage ("build") {
       steps {
	     echo "=============Build is in progress========"
          sh "mvn clean deploy -Dmaven.test.skip=true"
		 echo "=========Build completed======"
       }
	}
	stage ("Test of the job") {
	  steps {
	   echo "==========Testing of the Maven job=========="
	     sh "mvn surefire-report:report"
	   echo "+++++++++++Testing completed=========="
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
