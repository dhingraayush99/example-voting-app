pipeline {
    agent { label 'worker' }
    
    stages {
        stage("Docker Build") {
            steps {
                sh "echo Docker Build"
            }
        }
        
        stage("Docker Deploy") { // Fixed missing quote
            steps {
                sh "echo deploy"
            }
        }
    }
}
