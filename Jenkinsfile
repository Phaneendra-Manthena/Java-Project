@Library('my shared library') _
pipeline{

    agent any

    stages{
        stage('Git Checkout'){
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
                    steps{
                        script{
                            mvnTest()
                        }
                    }
                }
                stage('Integration Test'){
                    steps{
                        script{
                            integrationTest()
                        }
                    }
                }
                stage('Code Analysis With CheckStyle'){
                    steps{
                        script{
                            checkStyle()
                        }
                    }
                }
            }
        }
    