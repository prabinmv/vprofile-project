pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "JDK17"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.27.123'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vprofile-maven-grp'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archieving"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        // stage('Test') {
        //     steps {
        //         sh 'mvn -s settings.xml test'
        //     }
        // }

        // stage('Checkstyle') {
        //     steps {
        //         sh 'mvn -s settings.xml checkstyle:check' // Or use the maven plugin step if needed
        //     }
        // }
    }
}
