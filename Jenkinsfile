pipeline {
    agent any
    tools {
        maven "maven"
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "51.38.50.55:8081"
        NEXUS_REPOSITORY = "testmaven"
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
                                  file: 'target/applicationmaven-1.0.0.war',
                                  type: 'war'
                                ]
                            ],
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: 'org.sid',
                            version: '1.0.0',
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID                             
                    
                    }
                }
            }
        }
}
    

