@Library('my-shared-library') _

pipeline {
  agent any

  stages {
    stage('Git Checkout') {

      steps {
        script {
          gitCheckout(
            branch: 'main',
            url: 'https://github.com/kartheek2104/kartheek_dev.git'
          )
        }

      }
    }

    stage('Maven Unit test') {

      steps {
        script {
          mvnTest()
        }

      }
    }

     stage('Maven Integration test') {

      steps {
        script {
          mvnIntegrationTest()
        }

      }
    }
  }
}