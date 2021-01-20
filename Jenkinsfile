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
                docker.withRegistry('https://registry.hub.docker.com', DockerRegistry) {
                dockerImage.push()   
                }
            }
        }
    }
}
