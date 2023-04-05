@Library('my shared library') _
pipeline{

    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'phani997')
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
                     when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            def SonarQubecredentialsId = 'sonarapi'
                            qualityGateStatus(SonarQubecredentialsId)
                        }
                    }
                }
                stage('Maven Build'){
                     when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            mvnBuild()
                        }
                    }
                }
                stage('Docker Image Build'){
                     when { expression {  params.action == 'create' } }
                     steps{
                        script{
                       dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                        }
                     }
                }
                stage('Docker Image Scan'){
                    when { expression {  params.action == 'create' } }
                    steps{
                        script{
                            dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
                        }
                    }
                }
            }
        }
    