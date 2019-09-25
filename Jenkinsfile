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
				bat '${M2_HOME}/bin/mvn --batch-mode -V -U -e clean verify -Dsurefire.useFile=false -Dmaven.test.failure.ignore'
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
		stage('Static Code Analysis') { 
            steps {
				 
            }
        }
    }
}
