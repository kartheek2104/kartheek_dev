@Library('my-shared-library') _

pipeline {
  agent any

  parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'kartheek21')

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

    // stage('Maven Unit test') {
    // when { expression {  params.action == 'create' } }
    //   steps {
    //     script {
    //       mvnTest()
    //     }

    //   }
    // }

    //  stage('Maven Integration test') {
    //   when { expression {  params.action == 'create' } }

    //   steps {
    //     script {
    //       mvnIntegrationTest()
    //     }

    //   }
    // }
    // stage('Static code analysis: Sonarqube') {
    //   when { expression {  params.action == 'create' } }

    //   steps {
    //     script {
    //       def SonarQube = "sonarqube-api"
    //       statiCodeAnalysis(SonarQube)
    //     }

    //   }
    // }

    // stage('Quality Gate Status Check : Sonarqube') {
    //   when { expression {  params.action == 'create' } }

    //   steps {
    //     script {
    //       def SonarQube = "sonarqube-api"
    //       QualityGateStatus(SonarQube)
    //     }

    //   }
    // }

    stage('Maven Build : maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   mvnBuild()
               }
            }
        }
    stage('Docker Build Image'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                  dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }
    stage('Docker Image Scan: trivy '){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }
  }
}