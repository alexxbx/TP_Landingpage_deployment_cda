pipeline {
    agent any
    stages {
        stage('Continous Integration') {
            steps {
                git branch: 'main', url: 'https://github.com/alexxbx/TP_Landingpage_deployment_cda'
            }
        }
        stage ('controle qualité') {
            steps {
                sh """
                sonar-scanner -v
                """
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