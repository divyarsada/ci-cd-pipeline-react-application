def dockerImage = 'sampletest19/reactapp-pipeline'
pipeline{
    agent any
    stages{
        stage("Docker build"){
            steps{
                sh "docker build . -t dockerImage:$BUILD_NUMBER"
                }
        }  
        stage("Docker push"){
            steps{
                withDockerRegistry(credentialsId: 'DockerRegistry', url: 'https://registry.hub.docker.com') {
                         sh "docker push dockerImage:$BUILD_NUMBER"
                }    
            }
        }
    }
}
