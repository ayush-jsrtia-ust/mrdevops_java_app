@Library('my-shared-library') _

pipeline{

    agent any

    parameters{

        choice(
            name: 'action',
            choices: 'create\ndelete',
            description: 'Choose create/Destroy'
        )
    }

    stages{
        
        stage('Git Checkout'){

            when {
                expression { params.action == 'create' }
            }

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
        
        when {
            expression { params.action == 'create' }
        }

            steps{

                script{

                    mvnTest()
                }
            }
        }

        stage('Maven Integration Test'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    mvnIntegration()
                }
            }
        }

        stage('Static Code Analysis: SonarQube'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    def SonarQubecredentialsId = 'sonarqube-api'
                    staticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }

        stage('Quality Gate Status Check: SonarQube'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    def SonarQubecredentialsId = 'sonarqube-api'
                    QualityGateStatus(SonarQubecredentialsId)
                }
            }
        }
    }
}