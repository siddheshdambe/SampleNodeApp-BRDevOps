pipeline {
  agent any

  tools {
    nodejs 'NodeJS-18' // Name must match Jenkins global tool config
  }

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/siddheshdambe/SampleNodeApp-BRDevOps.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        sh 'npm test || echo "Tests failed"'
      }
    }

    stage('Build (optional)') {
      when {
        expression { fileExists('build') || fileExists('webpack.config.js') }
      }
      steps {
        echo 'Building app...'
        sh 'npm run build'
      }
    }

    stage('Run App') {
      steps {
        echo 'Starting the Node app (as background task)...'
        sh 'nohup node app.js > app.log 2>&1 &'
      }
    }

    // Optional deploy step
    stage('Deploy (optional)') {
      when {
        branch 'main'
      }
      steps {
        echo 'Deploy step - customize as needed'
        // Example: scp to server
        // sh 'scp -r * user@your-server:/var/www/my-node-app'
      }
    }
  }
}