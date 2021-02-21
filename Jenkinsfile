pipeline {
  agent any
environment { 
     PATH='/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/apache-maven-3.6.3/bin'
    }
  stages {
    stage('Compile') {
       steps {
	        sh "mvn compile"
       }
    }

    stage('Build') {
	     steps {
          sh "mvn package"
	     }
    }

    stage('Install') {
	     steps {
          sh 'mvn install'
	     }
    }

    stage('Archieve') {
        steps {
           archiveArtifacts 'target/*.jar'
        }
    }

    stage('FingerPrint') {
        steps {
           fingerprint 'target/*.jar'
        }
    }

    stage('HTML_Publish') {
	     steps {
	         junit 'target/surefire-reports/TEST-*.xml'
        }
    }

    stage ('Email') {
             steps {
                 emailext body: 'Build is completed', replyTo: 'hamzasohaib8@outlook.com', subject: 'Build is completed', to: 'hamzasohaib8@outlook.com'
        }
    }

  }

}
