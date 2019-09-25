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
                    set "M2_HOME = ${MAVEN_HOME}"
                '''
            }
        }
        stage('build') {
            steps {
				bat 'mvn --batch-mode -V -U -e clean verify -Dsurefire.useFile=false -Dmaven.test.failure.ignore'
            }
        }
		stage ('Analysis') {
            steps {
                bat 'mvn --batch-mode -V -U -e checkstyle:checkstyle pmd:pmd pmd:cpd findbugs:findbugs spotbugs:spotbugs'
            }
        }	
    }
	post {
        always {
			junit testResults: '**/target/surefire-reports/TEST-*.xml'

            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
            recordIssues enabledForFailure: true, tool: spotBugs()
            recordIssues enabledForFailure: true, tool: cpd(pattern: '**/target/cpd.xml')
            recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
        }
    }
}
