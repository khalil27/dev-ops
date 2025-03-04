pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://192.168.182.132:8081/repository/maven-releases/'
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
                    // Utilisation des credentials Jenkins de type Secret Text pour username et password
                    withCredentials([string(credentialsId: 'nexus-username', variable: 'NEXUS_USERNAME'),
                                     string(credentialsId: 'nexus-password', variable: 'NEXUS_PASSWORD')]) {
                        // Déploiement avec Maven en utilisant les identifiants
                        sh """
                        mvn deploy -DskipTests \
                            -Dnexus.username=${NEXUS_USERNAME} \
                            -Dnexus.password=${NEXUS_PASSWORD} \
                            -DaltDeploymentRepository=deploymentRepo::default::${NEXUS_URL}
                        """
                    }
                }
            }
        }
    }
}
