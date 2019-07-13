pipeline {
    agent any
    tools {
        maven 'maven'
	}
    stages {
        stage('Initialize') {
	steps {
	    echo 'validating source code...'
	    sh 'mvn validate'
	    }
	}
	stage('Build') {
	steps {
	    echo 'Building application package...'
	    sh 'mvn clean compile'
            }
        }
        stage('Test') {
	steps {
	    echo 'Starting Unit Test phase...'
	    sh 'mvn test'
	    }
	}
	stage('Packaging') {
	steps {
	    echo 'Starting packaging phase...'
	    sh 'mvn package verify install'
	    }
	}
	stage('Deploy') {
	steps {
	    echo 'Deploying package on tomcat...'
	    }
	}
  }
}
