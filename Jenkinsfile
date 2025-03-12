pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://192.168.182.132:8081/repository/maven-releases/'
        NEXUS_USERNAME = 'admin'
        NEXUS_PASSWORD = 'Khalil$200'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code from GitHub'
                git 'https://github.com/khalil27/dev-ops.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project using Maven'
                sh 'mvn clean install'
            }
        }

        stage('Deploy to Nexus') {
            steps {
                echo 'Deploying the artifact to Nexus Repository'
                sh """
                mvn deploy -X -DskipTests \
                    -DaltDeploymentRepository=deploymentRepo::default::http://${NEXUS_USERNAME}:${NEXUS_PASSWORD}@192.168.182.132:8081/repository/maven-releases/
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
        success {
            echo 'Deployment to Nexus was successful'
        }
        failure {
            echo 'Deployment to Nexus failed. Please check the logs for more details.'
        }
    }
}
