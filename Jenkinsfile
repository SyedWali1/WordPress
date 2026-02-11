pipeline {
    agent any


    stages {



        stage('Deploy wp-content') {
            steps {
                sh '''
                echo "Deploying wp-content..."

                # Remove old content safely
                rm -rf /var/www/html/wp-content/*

                # Copy new content from repo
                cp -r wp-content/* /var/www/html/wp-content/
                '''
            }
        }

        stage('Fix Permissions') {
            steps {
                sh '''
                echo "Fixing permissions..."

                chown -R www-data:www-data /var/www/html/wp-content
                chmod -R 755 /var/www/html/wp-content
                '''
            }
        }
    }
}


