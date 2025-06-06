pipeline {
    agent any

    environment {
        DIST_DIR = 'dist/angular-project'
        DEPLOY_DIR = '/var/www/html'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/phrygien/angular-jnkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Angular') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Assurez-vous que Jenkins peut exécuter sudo sans mot de passe (NOPASSWD dans sudoers)
                sh '''
                    if [ -d "$DIST_DIR" ]; then
                        echo "✅ Dossier $DIST_DIR trouvé. Déploiement..."
                        sudo rm -rf $DEPLOY_DIR/*
                        sudo cp -r $DIST_DIR/* $DEPLOY_DIR/
                        echo "✅ Déploiement terminé avec succès."
                    else
                        echo "❌ Le dossier $DIST_DIR n'existe pas."
                        exit 1
                    fi
                '''
            }
        }
    }

    post {
        failure {
            echo "❌ Le build ou le déploiement a échoué."
        }
        success {
            echo "✅ Tout est terminé avec succès."
        }
    }
}
