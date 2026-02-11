pipeline {
    agent any

    
    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'vm-ssh-key',
                    url: 'git@github.com:SyedWali1/WordPress.git'
            }
        }

        stage('Deploy wp-content') {
            steps {
                sh '''
                sudo rsync -av --delete wp-content/ /var/www/html/wp-content/
                '''
            }
        }

        stage('Fix Permissions') {
            steps {
                sh '''
                sudo chown -R www-data:www-data /var/www/html/wp-content
                sudo chmod -R 755 /var/www/html/wp-content
                '''
            }
        }
    }
}

