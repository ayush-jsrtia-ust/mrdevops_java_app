pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{

                script{

                    git branch: 'main', url: 'https://github.com/ayush-jsrtia-ust/mrdevops_java_app.git'
                }
            }
        }
    }
}