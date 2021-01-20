def dockerImage = 'sampletest19/reactapp-pipeline'
pipeline{
    agent any
    stages{
        stage("Docker build"){
            steps {
                script {
                    dockerImage = docker.build dockerImage + ":$BUILD_NUMBER"
                }
            }
        }  
        stage("Docker push"){
            steps{
                withDockerRegistry(credentialsId: 'DockerRegistry', url: 'https://registry.hub.docker.com') {
                dockerImage.push()
                }    
            }
        }
    }
}
