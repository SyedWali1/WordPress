pipeline {
    agent any

    
    stages {



        stage('Deploy wp-content') {
            steps {
                sh '''
                rm -rf /var/www/html/wp-content/*
                cp -r wp-content/* /var/www/html/wp-content/
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

