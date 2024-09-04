pipeline{
    agent any
    tools {
        jdk "OracleJDK11"
        maven "MAVEN3"
    }

    environment{
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '192.168.1.222'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexus'
    }

    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now Archiving..."
                    archiveArtifacts artifact:'**/*.war'
                }
            }
        }

        stage('Test'){
            steps{
                sh 'mvn -s settings.xml test'
            }
        }
    }
}