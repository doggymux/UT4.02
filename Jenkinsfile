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
        
        stage('Instalar Dependencias') {
            steps {
                sh 'cd angular/ && npm install --force'
                slackSend channel: '#tito-jenkins', color: 'good', message: 'niño tenemos npm funcionando'
            }
        }
        
        stage('Creamos la app') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/PPS/angular && ng build --prod'
                slackSend channel: '#el-tito-jenkins', color: 'good', message: 'muyayo no te lo vas a creer pero hacemos build'
            }
        }
        
        stage('Creamos la imagen de Docker') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/PPS/angular && docker build --build-arg DIST=dist/billingApp --build-arg CONFIG_FILE=nginx.conf -t doggy/anguloobstuso .'
                sh 'cd /var/lib/jenkins/workspace/PPS/java && docker build -t doggy/javasito .' 
                slackSend channel: '#tito-jenkins', color: 'good', message: 'Habemus docker'
            }
        }
    }
}
