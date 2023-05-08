pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git(
                    url: 'https://github.com/doggymux/UT4.02.git',
                    credentialsId: 'gitprueba',
                    branch: 'main'
                )
            }
        }
        stage('SonarQube analysis') {
            steps {
                echo 'Starting SonarQube analysis'
                withSonarQubeEnv('jenkins') {
                    echo 'Inside SonarQube environment'
                    sh '/sonar-scanner-4.8.0.2856-linux/bin/sonar-scanner \
                          -Dsonar.projectKey=jenkins \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=http://localhost:9000 \
                          -Dsonar.token=sqp_90ad91fbf79a4ca0313ee16544e024e6fa8aaedc'
                }
                echo 'Finished SonarQube analysis'
            }
        }
    }
}
