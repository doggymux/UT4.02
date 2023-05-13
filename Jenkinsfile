pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git(
                    url: 'https://github.com/doggymux/UT4.02.git',
                    credentialsId: 'github',
                    branch: 'main'
                )
            }
        }
        stage('SonarQube analysis') {
            steps {
                echo 'Starting SonarQube analysis'
                withSonarQubeEnv('sonarqube') {
                    echo 'Inside SonarQube environment'
                   
                    sh 'cd angular && /sonar-scanner-4.8.0.2856-linux/bin/sonar-scanner \
                            -Dsonar.projectKey=PPS-P4 \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.token=sqp_3640668c241c658c22f64659bf9103f51453d648'
                }
                echo 'Finished SonarQube analysis'
            }
        }
        
        stage('Despliegue') {
            steps {
                echo 'Desplegando dockers'
                sh 'cd angular && docker build .'
                echo 'Se terminó el despliegue de angular'
            }
        }
    }
}
