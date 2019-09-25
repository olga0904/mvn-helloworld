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
                    echo "M2_HOME = ${MAVEN_HOME}"
                '''
            }
        }
        stage('build') {
            steps {
				bat '${MAVEN_HOME}/bin/mvn --batch-mode -V -U -e clean verify -Dsurefire.useFile=false -Dmaven.test.failure.ignore'
            }
        }
		stage ('Analysis') {
            steps {
                bat '${M2_HOME}/bin/mvn --batch-mode -V -U -e checkstyle:checkstyle pmd:pmd pmd:cpd findbugs:findbugs spotbugs:spotbugs'
            }
        }
		
    }
}
