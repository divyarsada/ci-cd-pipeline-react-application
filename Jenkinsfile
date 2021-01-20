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
                withDockerRegistry(credentialsId: 'DockerRegistry', url: 'https://registry.hub.docker.com') {
                         sh "docker push sampletest19/reactapp-pipeline:${BUILD_NUMBER}"
                }    
            }
        }
    }
}
