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
                withSonarQubeEnv('sonarqube') {
                    echo 'Inside SonarQube environment'
                    sh '/sonar-scanner-4.8.0.2856-linux/bin/sonar-scanner \
                            -Dsonar.projectKey=jenkins \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.token=sqp_decb333a59e814f689d9a3d509e354c41641d715'
                }
                echo 'Finished SonarQube analysis'
            }
        }
    }
}
