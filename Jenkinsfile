@Library('my shared library') _
pipeline{

    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')

    }

    stages{
        stage('Git Checkout'){
            when { expression {  params.action == 'create' } }
            steps{
                script{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/Phaneendra-Manthena/Java-Project.git"
                    )
                        }
                    }
                }
                stage('Unit Test'){
                    when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            mvnTest()
                        }
                    }
                }
                stage('Integration Test'){
                    when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            integrationTest()
                        }
                    }
                }
                stage('Code Analysis With CheckStyle'){
                    when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            checkStyle()
                        }
                    }
                }
                stage('Static Code Analysis'){
                    when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            def SonarQubecredentialsId = 'sonarapi'
                            staticCodeAnalysis(SonarQubecredentialsId)
                        }
                    }
                }
                stage('Quality Gate Status Check'){
                    steps{
                        script{
                            def SonarQubecredentialsId = 'sonarapi'
                            qualityGateStatus(SonarQubecredentialsId)
                        }
                    }
                }
                stage('Maven Build'){
                    steps{
                        script{
                            mvnBuild()
                        }
                    }
                }
            }
        }
    