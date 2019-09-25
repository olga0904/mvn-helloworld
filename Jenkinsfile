node {
    stage ('Checkout') {
        git branch:'master', url: 'git@github.com:olga0904/mvn-helloworld.git'
    }
    stage ('Build') {
        def M2_Home = tool 'maven 3.6.2'

        bat "${M2_Home}/bin/mvn --batch-mode -V -U -e clean verify -Dsurefire.useFile=false"

        junit testResults: '**/target/*-reports/TEST-*.xml'

        def java = scanForIssues tool: java()
        def javadoc = scanForIssues tool: javaDoc()
        
        publishIssues issues: [java, javadoc], filters: [includePackage('io.jenkins.plugins.analysis.*')]
    }
