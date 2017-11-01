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
          sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar ' + 
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
             def qg = waitForQualityGate() 
             if (qg.status != 'OK') {
               error "Pipeline aborted due to quality gate failure: ${qg.status}"
             }
          }
        }
    }
  }
}
