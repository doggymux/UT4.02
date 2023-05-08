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
                            -Dsonar.host.url=http://172.17.0.3:9000 \
                            -Dsonar.token=sqp_327484a14c100683cc0a6eaa3b5545a77bcfa2be'
                }
                echo 'Finished SonarQube analysis'
            }
        }
    }
}
