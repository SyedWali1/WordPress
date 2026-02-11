pipeline {
    agent any

    stages {

        stage('Deplooy wp-content') {
            steps {
                sh '''
                echo "Deploying wp-content..."
                rm -rf /var/www/html/wp-content/*
                cp -r wp-content/* /var/www/html/wp-content/
                '''
            }
        }
    }
}



