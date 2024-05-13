pipeline {
  agent any
  stages {
      stage('Build') {
        steps {
          sh 'mvn -B -DskipTests clean package'
        }
      }
      stage('pmd') {
        steps {
          sh 'mvn pmd:pmd'
        }
      }
      stage('Doc') {
        steps {
          sh 'mvn javadoc:javadoc --fail-never'
        }
      }
      stage('Test Report') {
        steps {
          sh 'mvn -Dtest=TestCss test --fail-never'
          sh 'mvn surefire-report:report'
        }
      }
  }
  post {
    always {
      archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    }
  }
}