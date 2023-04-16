@Library('my-shared-library') _

pipeline {
  agent any

  parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        
    }

  stages {
    when { expression {  params.action == 'create' } }
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
    when { expression {  params.action == 'create' } }
      steps {
        script {
          mvnTest()
        }

      }
    }

     stage('Maven Integration test') {
      when { expression {  params.action == 'create' } }

      steps {
        script {
          mvnIntegrationTest()
        }

      }
    }
  }
}