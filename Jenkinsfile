pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://192.168.182.132:8081//repository/maven-releases/'
        NEXUS_USERNAME = credentials('nexus-username')
        NEXUS_PASSWORD = credentials('nexus-password')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/khalil27/dev-ops.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                script {
                    // Deploy to Nexus via Maven with authentication
                    sh """
                    mvn deploy -DskipTests -DnexusUsername=${NEXUS_USERNAME} -DnexusPassword=${NEXUS_PASSWORD}
                    """
                }
            }
        }
    }
}
192.168.56.10