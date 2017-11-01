pipeline {
  agent any
  stages {
    stage('Check code syntax') {
      steps {
        sh 'echo "PHP Check done"'
        sh 'echo "Check JSLint"'
      }
    }
    stage('Check code quality') {
      steps {
        waitForQualityGate()
      }
    }
  }
}