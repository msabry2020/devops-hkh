def COLOR_MAP = [
        'SUCCESS': 'good',
        'FAILURE': 'danger'
]

pipeline{
    agent any
    tools {
        jdk "OracleJDK17"
        maven "MAVEN3"
    }

    environment{
        SNAP_REPO = 'vprofile-snapshot'
		#NEXUS_USER = 'admin'
		#NEXUS_PASS = 'admin'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '127.0.0.1'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexus'
        REGISTRY = 'msabry/cd-app'
        registryCredential = 'dockerhub_ID'
    }

    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now Archiving..."
                    archiveArtifacts artifacts:'**/*.war'
                }
            }
        }

        stage('Test'){
            steps{
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Upload Artifacts'){
            steps{
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${NEXUSIP}:${NEXUSPORT}",
                    groupId: 'QA',
                    version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                    repository: "${RELEASE_REPO}",
                    credentialsId: "${NEXUS_LOGIN}",
                    artifacts: [
                        [artifactId: 'vproapp',
                        classifier: '',
                        file: 'target/vprofile-v2.war',
                        type: 'war']
                    ]
                )      
            }
        }

        stage('Build App Image'){
            steps{
                script{
                    dockerImage = docker.build(REGISTRY + ":$BUILD_NUMBER", "./Docker-files/app/")
                }
            }
        }
        stage('Upload App image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }
                }
            }
        }

    }

    post {
        always{
            slackSend(
                channel: "#cicd", 
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}* job ${env.JOB_NAME} build ${env.BUILD_ID} \n ${BUILD_URL}"
                )
        }
    }
}
