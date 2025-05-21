pipeline {
  agent any

  tools {
    nodejs 'NodeJS-18' // Must match what you configured
  }

  stages {
    stage('Install dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run application') {
      steps {
        bat 'start "NodeApp" cmd /c "node index.js"'

        bat 'ping 127.0.0.1 -n 60 > nul'

        bat 'taskkill /F /IM node.exe || echo Node was already stopped'
      }
    }
    
      stage('Build complete') {
      steps {
        echo 'Build completed successfully.'
      }
    }
  }
}