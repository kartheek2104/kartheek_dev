@Library('my-shared-library')
pipeline{
    agent any

    stages{
     stage('Git Checkout'){

        steps{
            script{
                gitCheckout{
                    branch: "main"
                    url: 'https://github.com/kartheek2104/kartheek_dev.git'
                }
            }

    }
}
}
}