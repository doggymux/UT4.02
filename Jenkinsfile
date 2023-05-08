pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git(
                    url: 'https://github.com/JMontRod/UT4.PC2-G3-Apps.git',
                    credentialsId: 'gitprueba',
                    branch: 'main'
                )
            }
        }
        stage('SonarQube analysis') {
            steps {
                echo 'Starting SonarQube analysis'
                withSonarQubeEnv('sq1') {
                    echo 'Inside SonarQube environment'
                    sh '/sonar-scanner-4.8.0.2856-linux/bin/sonar-scanner \
                        -Dsonar.projectKey=TEST \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://172.17.0.2:9000 \
                        -Dsonar.login=sqp_17b1e31159b43e3416895b7c8532cdc3c5050bad'
                }
                echo 'Finished SonarQube analysis'
            }
        }
    }
}
