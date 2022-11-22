pipeline {
    agent any
    tools {
        maven "maven"
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "192.168.34.100:8081"
        NEXUS_REPOSITORY = "maven-nexus-repo"
        NEXUS_CREDENTIAL_ID = "nexus-cred"
    }
    stages {
        stage("Clone code from VCS") {
            steps {
                script {
                    git 'https://github.com/sadokkhemila/appmavennexus.git';
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
        stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    
                          nexusArtifactUploader artifacts: [
                           
                                [
                                  artifactId: 'applicationmaven',
                                  classifier: '',
                                  file: 'target/applicationmaven-0.0.1-SNAPSHOT.jar',
                                  type: 'jar'
                                ]
                            ],
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: 'org.sid',
                            version: '0.0.1-SNAPSHOT',
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID                             
                    
                    }
                }
            }
        }
}
    

