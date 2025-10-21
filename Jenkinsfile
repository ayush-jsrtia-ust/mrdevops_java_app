@Library('my-shared-library') _

pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{

                script{

                    gitCheckout(
                        branch: 'main',
                        url: 'https://github.com/ayush-jsrtia-ust/mrdevops_java_app.git'
                    )
                }
            }
        }

        stage('Maven Unit Test'){

            steps{

                script{

                    mvnTest()
                }
            }
        }

        stage('Maven Integration Test'){

            steps{

                script{

                    mvnIntegration()
                }
            }
        }
    }
}