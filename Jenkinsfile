pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {
        stage('GIT') {
            steps {
                git(
                    branch: 'master',
                    url: 'https://github.com/khalil27/dev-ops.git'
                )
            }
        }
                stage('compile') {
            steps {
                echo "🛠️ Compilation du projet avec Maven..."
                sh 'mvn clean compile'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.token=squ_c1510c00ca013d4e37ea3aab9a89c9b683915e2a -Dmaven.test.skip=true'
            }
        }
        stage('Deploy to Nexus') {
            steps {
                echo "🚀 Déploiement de l'artefact sur Nexus..."
                sh 'mvn deploy -Dmaven.test.skip=true'
            }
        }
    }
}

