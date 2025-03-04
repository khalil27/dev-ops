pipeline {
    agent any

    environment {
        NEXUS_URL = 'http://192.168.182.132:8081/repository/maven-releases/'
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
                script {
                    // Utilisation des credentials Jenkins pour récupérer le nom d'utilisateur et le mot de passe
                    withCredentials([string(credentialsId: 'nexus-username', variable: 'NEXUS_USERNAME'),
                                     string(credentialsId: 'nexus-password', variable: 'NEXUS_PASSWORD')]) {
                        echo 'Deploying the artifact to Nexus Repository'

                        // Déploiement avec les logs détaillés (mode debug Maven)
                        sh """
                        mvn deploy -X -DskipTests \
                            -Dnexus.username=${NEXUS_USERNAME} \
                            -Dnexus.password=${NEXUS_PASSWORD} \
                            -DaltDeploymentRepository=deploymentRepo::default::${NEXUS_URL}
                        """
                    }
                }
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
