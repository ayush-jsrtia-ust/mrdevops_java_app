@Library('my-shared-library') _

pipeline{

    agent any

    parameters{

        choice(
            name: 'action',
            choices: 'create\ndelete',
            description: 'Choose create/Destroy'
        )
        string(
            name: 'ImageName',
            description: 'Enter the Image Name',
            defaultValue: 'java_app'
        )
        string(
            name: 'ImageTag',
            description: 'Enter the Image Tag',
            defaultValue: 'v1'
        )
        string(
            name: 'DockerHubUser',
            description: 'Enter the Docker Hub Username',
            defaultValue: 'ayushjsrtia'
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

        stage('Maven Build'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    mvnBuild()
                }
            }
        }

        stage('Docker Image Build'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    dockerBuild(
                        "${params.ImageName}",
                        "${params.ImageTag}",
                        "${params.DockerHubUser}"
                    )
                }
            }
        }

        stage('Docker Image Scan: Trivy'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    dockerImageScan(
                        "${params.ImageName}",
                        "${params.ImageTag}",
                        "${params.DockerHubUser}"
                    )
                }
            }
        }

        stage('DockerHub Login and Push'){

            when {
                expression { params.action == 'create' }
            }

            steps{

                script{

                    dockerPush(
                        "${params.ImageName}",
                        "${params.ImageTag}",
                        "${params.DockerHubUser}"
                    )
                }
            }
        }
    }
}