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
      stage('Test') {
        steps {
          sh 'mvn test --fail-never'
        }
      }
      stage('Test Report') {
        steps {
          sh 'mvn surefire-report:report'
        }
      }
      stage('Doc') {
        steps {
          sh 'mvn javadoc:jar --fail-never'
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