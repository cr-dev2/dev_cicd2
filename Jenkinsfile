pipeline {
  agent any
  
  parameters {
	string(
		name: 'Path01',
		defaultValue:'Bala',
		description: 'Where to put the build!')
    }
  
  stages {
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/develop']],
                     userRemoteConfigs: [[credentialsId: 'f1a093d8-cb3d-467a-b0f3-670289e8bc6e'],[url: 'https://github.com/cr-dev2/dev_cicd2.git']]])
        echo 'Hello '
      }
    }
    stage('Build') {
      steps {
        echo 'Build is Starting'
        sh 'mvn -U install -DskipTests=true'
        echo 'Build Completed'
      }
    }
    stage('unit Test') {
      steps {
        echo 'Tests are Starting'
        sh 'mvn test'
        echo 'Tests are Completed'
      }
    }
	stage('SonarQube Rules Execution') {
		steps {
			echo 'SonarQube Rules Execution started'
			withSonarQubeEnv('SonarServer-Local') {
				sh 'mvn sonar:sonar'
			}
			echo 'SonarQube Rules Execution Completed'
		}
	}
	
	stage('Artifact Copy To Nexus')
	{
		steps{
			echo 'Artifact Copy to Nexus Started'
			nexusArtifactUploader(
				nexusVersion: 'nexus3',
				protocol: 'http',
				nexusUrl: '52.209.36.199:8081',
				groupId: 'com.mycompany',
				version: '1.0.0-SNAPSHOT',
				repository: 'CICDREPO/',
				credentialsId: 'CostaPOCNexus',
				artifacts: [
					[artifactId: 'cicdeautodeployproj',
					 classifier: '',
					 file: 'target/cicdeautodeployproj-1.0.0-SNAPSHOT.zip',
					 type: 'zip']
				]
			 )
			echo 'Artifact Copy to Nexus Completed'
		}
	}
	stage('CloudHub Auto-Deploy') {
      steps {
		echo 'CloudHub Auto-Deploy Starting'
        sh 'mvn deploy'
        echo 'CloudHub Auto-Deploy Completed'
      }
    }
	stage('Alerts & Notifications') {
      steps {
		echo 'Send Alert to Owner Starting 04'
        echo 'Send Alert to Owner Completed 04'
      }
    }
  }
}