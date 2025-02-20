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
                    url: 'https://github.com/khalil27/dev-ops.git',
                    credentialsId: 'jenkins-example-github-pat'
                )
            }
        }
    }
}

