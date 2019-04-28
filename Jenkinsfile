pipeline{
    agent any
    ws('/opt/codebase') 
    stages{
        stage("SCM Checkout"){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/sharif59/Repo1.git']]])
            }
            post{
                always{
                    echo "Stage 1"
                }
                success{
                    echo "SCM checkout has domne succesfully"
                }
                failure{
                    echo "SCM Checkout Has failed"
                }
            }
        }
        stage("SCm checkout B"){
            steps{
                 script {
                    // some block
                    if (fileExists ('SCM-B')){
                        echo 'Macaw-core directory already exist'
                    }
                    else {
                        sh label: '', script: 'mkdir SCM-B'
                    }

                }
                dir('SCM-B') {
                    //BitBucket Code for Macaw-Core
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/sharif59/gitdemo.git']]])
                    
                }
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++A executed succesfully++++===="
                }
                failure{
                    echo "====++++A execution failed++++===="
                }
        
            }
        }
        stage("execute shell"){
            steps{
                echo "hello It is in stage 2"
            }
            post{
                always{
                    echo "Stage2"
                }
                success{
                    echo "Executed shell successfully"
                }
                failure{
                    echo "====++++execute shell execution failed++++===="
                }
        
            }
        }
        stage("Downstream Job B"){
            steps{
                build 'JobB'
            }
            post{
                always{
                    echo "Job B"
                }
                success{
                    echo "Job success"
                }
                failure{
                    echo "====++++A execution failed++++===="
                }
        
            }
        }
    }
    
    post{
        always{
            echo "========always ========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
