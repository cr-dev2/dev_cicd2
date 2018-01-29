pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/develop']],
                     userRemoteConfigs: [[credentialsId: '9d379816-40aa-43ff-9f6c-8015f4936219'],[url: 'https://github.com/cr-dev2/dev_cicd2.git']]])
        echo 'Hello World'
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
	stage('sonar quality gate') {
      steps {
		echo 'CloudHub Auto-Deploy Starting'
        sh 'mvn deploy'
        echo 'CloudHub Auto-Deploy Completed'
      }
    }
  }
  }
}