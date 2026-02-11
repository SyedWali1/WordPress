pipeline {
    agent any

    environment {
        DEPLOY_PATH = "/var/www/html"
        
    }
    stages {

        stage('Deploy wp-content') {
            steps {
                sh '''
                echo "Syncing wp-content..."
                rsync -av --delete wp-content/ ${DEPLOY_PATH}/wp-content/
                '''
            }
        }

        stage('Fix Permissions') {
            steps {
                sh '''
                echo "Fixing permissions..."
                sudo chown -R www-data:www-data ${DEPLOY_PATH}
                sudo chmod -R 755 ${DEPLOY_PATH}
                '''
            }
        }

        stage('Restart Apache') {
            steps {
                sh '''
                echo "Restarting Apache..."
                sudo systemctl restart apache2
                '''
            }
        }
    }
}
