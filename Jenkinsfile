pipeline {
    agent any
    tools {
        maven 'Maven 3.6.2'
        jdk 'Java8'
    }
    stages {
		stage ('Initialize') {
            steps {
                bat '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('build') {
            steps {
				bat 'mvn -B -DskipTests clean package'
            }
        }
		stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
		stage('Deliver') { 
            steps {
				bat './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
