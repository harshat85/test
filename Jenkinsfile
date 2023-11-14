pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                sh 'jmeter -n -t my_test_plan.jmx'
            }
        }
		        stage('Sonar') {
            steps {
                sh 'sonarscanner'
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook credentialsId: 'my-ansible-credentials', inventory: 'my-inventory', playbook: 'deploy.yml'
            }
        }
    }
}
