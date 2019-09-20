pipeline {
    agent any
	 tools {
        maven 'Maven 3.6.2'
        jdk 'Java8'
    }
    stages {
        stage('build') {
            steps {
				bat 'mvn -B -DskipTests clean package'
            }
        }
    }
}