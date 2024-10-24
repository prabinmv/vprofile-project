pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUS_VERSION = "nexus3"
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin'
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "172.31.27.123:8081"
        NEXUS_REPOSITORY = "vprofile-release"
        NEXUS_CREDENTIAL_ID = "nexuslogin"
        
    }

    stages { 
        stage ('Build'){
            steps {
               sh 'mvn -s settings.xml -DskipTests install' 
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
                
            }
        }
        stage ('Test'){
            steps {
                sh 'mvn test'
            }
        }
        stage ('Checkstyle Analysis') {
            steps {
                sh  'mvn  checkstyle:checkstyle'
            }
        }
    }
}