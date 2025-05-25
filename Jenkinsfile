pipeline{
    agent{label 'worker'}
    stages{
        stage("Docker build and push"){
            steps{
                sh "docker login -u dhingra07 -p Yourp@sscode@789"
                sh '''
                    cd vote
                    docker build -t dhingra07/vote:v${BUILD_NUMBER} .
                    '''
                sh "docker push dhingra07/vote:v${BUILD_NUMBER}"
            }
        }
        stage("Deploy"){
            steps{
                sh "echo docker deploy"
            }
        }
    }
}
