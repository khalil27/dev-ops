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
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=Khalilyosr!200 -Dmaven.test.skip=true';
            }
        }
    }
}

