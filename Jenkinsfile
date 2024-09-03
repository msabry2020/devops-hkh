pipeline{
    agent any
    tools {
        jdk "OracleJDK11"
        maven "MAVEN3"
    }

    environment{
        SNAP-REPO = 'snapshot'
		NEXUS-USER = 'admin'
		NEXUS-PASS = 'admin'
		RELEASE-REPO = 'vprofile-release'
		CENTRAL-REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.86.7'
		NEXUSPORT = '8081'
		NEXUS-GRP-REPO = 'vpro-maven-group'
        NEXUS-LOGIN = 'nexus'
    }

    stages{
        stage('Build'){
            steps{
                sh "mvn -s settings.xml -DskipTests install"
            }
        }
    }
}