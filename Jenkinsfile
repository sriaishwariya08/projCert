pipeline {
    agent any
    stages {

        stage('Install Docker via Ansible') {
            steps {
                sh 'ansible-playbook -i ~/ansible/hosts ~/ansible/install_docker.yml'
            }
        }

        stage('Build & Deploy PHP Container') {
            steps {
                sh '''
                cd ~/projCert
                git pull || git clone https://github.com/sriaishwariya08/projCert.git ~/projCert
                docker build -t php-app .
                docker run -d --name php-container -p 80:80 php-app
                '''
            }
        }
    }
    post {
        failure {
            sh '''
            docker rm -f php-container || true
            '''
        }
    }
}

