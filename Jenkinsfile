pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                sshagent(['my-ssh-key']) {
                    sh 'ssh my-server "cd /var/www/my-app && git pull && npm install && pm2 restart my-app"'
                }
            }
        }
    }
}
