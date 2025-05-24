pipeline {
    agent any

    environment {
      NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
      NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
  }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/siddheshdambe/SampleNodeApp-BRDevOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Netlify') {
            steps {
                sh 'npx netlify deploy --prod --auth $NETLIFY_AUTH_TOKEN --site $NETLIFY_SITE_ID'
            }
        }
    }
}
