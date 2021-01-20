def dockerImage = 'sampletest19/reactapp-pipeline'
pipeline{
    agent {label 'slave1'}
    stages{
        stage("Docker build"){
            steps{
                sh "docker build . -t sampletest19/reactapp-pipeline:${BUILD_NUMBER}"
                }
        }  
        stage("Docker push"){
            steps{
                withCredentials([string(credentialsId: 'DockerHub', variable: 'DockerHubPwd')]) {
                    sh "docker login -u sampletest19 -p ${DockerHubPwd}"
                }
                sh "docker push sampletest19/reactapp-pipeline:${BUILD_NUMBER}"
            }
        }
    }
}
