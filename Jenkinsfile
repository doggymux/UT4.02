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
                            -Dsonar.host.url=http://172.17.0.2:9000 \
                            -Dsonar.token=sqp_decb333a59e814f689d9a3d509e354c41641d715'
                    
                    sh 'cd angular && /sonar-scanner-4.8.0.2856-linux/bin/sonar-scanner \
                            -Dsonar.projectKey=Angular \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://127.17.0.2:9000 \
                            -Dsonar.token=sqp_c7d7f4d68502747a508c21351ec54edbaab57a77'
                }
                echo 'Finished SonarQube analysis'
            }
        }
    }
}
