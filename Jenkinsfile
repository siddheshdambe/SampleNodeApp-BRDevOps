pipeline {
    agent any

    environment {
      NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
      NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/siddheshdambe/SampleNodeApp-BRDevOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Install Netlify CLI') {
            steps {
                sh 'npm install -g netlify-cli'
            }
        }

        stage('Build Project') {
            steps {
                // Skip or update this if your app doesn’t need to be built
                sh 'npm run build'
            }
        }

        stage('Deploy to Netlify') {
            steps {
                sh '''
                    netlify deploy --prod \
                    --dir=build \
                    --site=$NETLIFY_SITE_ID \
                    --auth=$NETLIFY_AUTH_TOKEN
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment to Netlify successful!'
        }
        failure {
            echo '❌ Deployment failed. Check the logs above.'
        }
    }
}
