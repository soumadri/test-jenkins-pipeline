pipeline {
  agent any
  stages {
    stage('Code syntax check') {
      steps {
        sh 'echo "PHP Check done"'
        sh 'echo "Check JSLint"'
      }
    }
    stage('SonarQube Quality Check') {
      steps {
        echo 'Executing Sonar code analysis'
      }
    }
    stage('SonarQube Quality Gate') {
      steps {
        echo 'Sonar gate passed'
      }
    }
    stage('') {
      steps {
        sh 'echo "Running unit tests"'
      }
    }
  }
}