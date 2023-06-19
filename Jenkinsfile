pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                ansiblePlaybook(playbook: 'install_docker.yaml')
            }
        }
        
        stage('Deploy App') {
            steps {
                ansiblePlaybook(playbook: 'deploy_app.yaml')
            }
        }
        
        stage('Deploy DB') {
            steps {
                ansiblePlaybook(playbook: 'deploy_db.yaml')
            }
        }
        
        stage('Push App Image') {
            steps {
                ansiblePlaybook(playbook: 'push_app_image.yaml')
            }
        }
    }

    post {
        success {
            stage('Cleanup') {
                steps {
                    ansiblePlaybook(playbook: 'cleanup_app_server.yaml')
                }
            }
        }
    }
}

