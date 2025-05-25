pipeline {
    agent { label 'worker' }
    
    options { 
        buildDiscarder(logRotator(numToKeepStr: '15'))
        disableConcurrentBuilds()
        retry(2)
        timeout(time: 10, unit: 'MINUTES')
    }
    
    parameters {
        string(name: 'BRANCH', defaultValue: 'develop', description: '') // Fixed typo: 'BRNACH' → 'BRANCH'
        booleanParam(name: 'TEST_CASES', defaultValue: true, description: '')
        choice(name: 'ENV', choices: ['dev', 'qa', 'uat'], description: '')
    }
    
    stages {
        stage("Docker build and push") {
            steps {
                sh "docker login -u dhingra07 -p asasa9"
                sh '''
                    cd vote
                    docker build -t dhingra07/vote:v${BUILD_NUMBER} .
                '''
                sh "docker push dhingra07/vote:v${BUILD_NUMBER}"
            }
        }

        stage("Parallel testing") {
            parallel {
                stage("Linux Test") {
                    steps {
                        sh "echo linux"
                        sh "sleep 180"
                    }
                }  

                stage("Windows Test") {
                    steps {
                        sh "echo windows"
                        sh "sleep 180"
                    }
                }  
            } // Closed parallel block properly
        }

        stage("Deploy") { // Fixed incorrect nesting
            steps {
                sh "echo docker deploy"
            }
        }
    }
}
