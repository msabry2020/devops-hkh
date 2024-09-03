pipeline{
    agent any
    tools {
        jdk "OracleJDK11"
        maven "MAVEN3"
    }

    environment{
        SNAP_REPO = 'snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.86.7'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexus'
    }

    stages{
        stage('Build'){
            steps{
                sh "mvn -s settings.xml -DskipTests install"
            }
        }
    }
}