pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Remplacer 'main' si ta branche s'appelle autrement
                git branch: 'main', url: 'https://github.com/phrygien/angular-jnkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Angular') {
            steps {
                sh 'npm run build --prod'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r dist/angular-project/* /var/www/html/
                '''
            }
        }
    }
    post {
        failure {
            echo '❌ Le build ou le déploiement a échoué.'
        }
    }
}
