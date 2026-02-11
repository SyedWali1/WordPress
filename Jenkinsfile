pipeline {
    agent any

    environment{
        DEPLOY_PATH = "/var/www/html"
        GIT_REPO = "git@github.com:SyedWali1/WordPress.git"
        BRANCH = "main"
    }

    stages{
        stage('Checkout SCM') {
            steps{
                git branch: "${BRANCH}",
                    url: "${GIT_REPO}"
            }
        }

        stage('Deploy wp-content via SSH') {
            steps{
                sshagent(credentials: ['vm-ssh-key']) {
                    sh '''
                    echo "Syncing wp-content to VM..."

                    rsync -avz --delete \
                    wp-content/ \
                    digital925@localhost:${DEPLOY_PATH}/wp-content/
                    '''
                }
            }
        }

        stage('Fix Permissions') {
            steps {
                sshagent(credentials: ['vm-ssh-key']) {
                    sh'''
                    ssh digital925@localhost "
                        sudo chown -R www-data:www-data ${DEPLOY_PATH} &&
                        sudo chmod -R 755 ${DEPLOY_PATH}
                    "
                    '''
                    
                }
            }
        }

        stage('Restart Apache') {
            steps{
                sshagent(credentials:['vm-ssh-key']) {
                    sh '''
                    ssh digital925@localhost "sudo systemctl restart apache2"
                    '''
                }
            }
        }
    }
}