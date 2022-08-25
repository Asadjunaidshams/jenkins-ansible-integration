pipeline {
    agent any
    tools {
	    maven 'MAVEN_HOME'
	}
    stages {
        stage('SCM-Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-credentials', 
                url: 'https://github.com/Asadjunaidshams/jenkins-ansible-integration.git'    
            }
        }
		stage('Clean-compile') {
            steps {
                sh "mvn clean compile"   
            }
        }
		stage('package') {
            steps {
                sh "mvn package"
            }
        }
        stage('Ansible-Deployment') {
            steps {
                ansiblePlaybook become: true, credentialsId: 'ec2-user',
				disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts', playbook: 'install-httpd.yml'
            }
        }
    }
}

