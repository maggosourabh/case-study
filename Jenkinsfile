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
	    sshagent(['tomcat-deploy']) {
	    sh 'scp -o StrictHostKeyChecking=no target/*.war centos@172.31.88.229:/tmp'
	    sh 'ssh -o StrictHostKeyChecking=no centos@172.31.88.229 "sudo rm -rf /opt/tomcat/webapps/*"'
	    sh 'ssh -o StrictHostKeyChecking=no centos@172.31.88.229 "sudo mv /tmp/*.war /opt/tomcat/webapps"'
	       }
	    }
	}
  }
}
