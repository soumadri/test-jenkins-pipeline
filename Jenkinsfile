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
        withSonarQubeEnv('SonarQube'){
          sh 'mvn sonar:sonar ' + 
            '-f all/pom.xml ' +
            '-Dsonar.projectKey=test ' +
            '-Dsonar.login=admin ' +
            '-Dsonar.password=admin ' +
            '-Dsonar.language=php ' +
            '-Dsonar.sources=. ' +
            '-Dsonar.tests=. ' 
        }
      }
    }
    stage("SonarQube Quality Gate") { 
        steps {
          timeout(time: 1, unit: 'HOURS') { 
             script {
               def qg = waitForQualityGate() 
               if (qg.status != 'OK') {
                 error "Pipeline aborted due to quality gate failure: ${qg.status}"
               }
             }
          }
        }
    }
  }
}
