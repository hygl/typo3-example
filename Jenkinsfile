pipeline {
  agent any
  stages {
    stage('get composer') {
      steps {
        sh 'curl -LO https://getcomposer.org/download/2.1.8/composer.phar'
        sh 'echo 77b8aca1b41174a67f27be066558f8a96f489916f4cded2bead3cab6a3f33590 composer.phar | sha256sum  --check --status'
      }
    }
    stage('build') {
      steps {
        sh 'php composer.phar install'
        sh 'zip -r typo3-example-$BUILD_NUMBER.zip vendor/'
        sh 'zip -r typo3-example-$BUILD_NUMBER.zip public/'
        sh 'zip -r typo3-example-$BUILD_NUMBER.zip var/'
        sh 'zip -r typo3-example-$BUILD_NUMBER.zip config/'
      }
      post {
        success {
          archiveArtifacts artifacts: 'typo3-example-*.zip', fingerprint: true
        }
      }
    }
  }
}
