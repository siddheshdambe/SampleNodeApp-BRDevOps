pipeline {
    agent any
 
    environment {
        NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
        NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
        PUBLISH_DIRECTORY = 'build'
    }
 
    stages {
        stage('Build') {
            steps {
                script {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }
 
 
        stage('Deploy to Netlify') {
            steps {
                script {
                    bat 'npm install -g netlify-cli'
                    bat 'netlify login --auth %NETLIFY_AUTH_TOKEN%'
                    bat 'netlify deploy --prod -s %SITE_ID% --dir=%PUBLISH_DIRECTORY%'
                }
            }
        }
    }
}
