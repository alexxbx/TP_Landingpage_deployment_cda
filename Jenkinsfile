pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }
    stages {
        stage('Continous Integration') {
            steps {
                git branch: 'main', url: 'https://github.com/alexxbx/TP_Landingpage_deployment_cda'
            }
        }
        stage ('controle qualité') {
            steps {
                sh '''
                sonar-scanner \
                    -Dsonar.projectKey=alex-tp-landingpage \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=https://669b-212-114-26-208.ngrok-free.app \
                    -Dsonar.token=$SONAR_TOKEN
                '''
            }
        }
        stage('Deploy via FTP') {
            steps {
                sh """
                    lftp -d -u alex3,${password} ftp-alex3.alwaysdata.net -e "
                        mirror -R /home/jenkins/workspace/alex-tp-landingpage/ www/;
                        bye
                    "
                """
            }
        }
    }
}