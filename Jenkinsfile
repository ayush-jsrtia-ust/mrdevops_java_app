@Library('my-shared-library') _

pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{

                script{

                    gitCheckout(
                        branch: 'main',
                        repositoryUrl: 'https://github.com/ayush-jsrtia-ust/mrdevops_java_app.git'
                    )
                }
            }
        }
    }
}