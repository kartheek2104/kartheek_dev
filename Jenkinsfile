@Library('my-shared-library') _

pipeline {
  agent any

  parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')

        }

  stages {
   
    stage('Git Checkout') {
      when { expression {  params.action == 'create' } }
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
    stage('static code analysis sonar') {
      when { expression {  params.action == 'create' } }

      steps {
        script {
          def SonarQube = "sonarqube-api"
          statiCodeAnalysis(SonarQube)
        }

      }
    }

    stage('Quality Gate analysis sonar') {
      when { expression {  params.action == 'create' } }

      steps {
        script {
          def SonarQube = "sonarqube-api"
          QualityGateStatus(SonarQube)
        }

      }
    }

    stage('Maven Build : maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   mvnBuild()
               }
            }
        }
  }
}