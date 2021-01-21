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
        stage("Deploy containerto ec2-instance"){
           steps{
               ansiblePlaybook credentialsId: 'ec2', disableHostKeyChecking: true, extras: "-e BUILD_NUMBER=${BUILD_NUMBER}", installation: 'ansible', inventory: 'react.inv', playbook: 'deploy-docker.yml'
           }
        }
        stage("Deploy to Kubernetes EKS Cluster"){
            steps{
                kubernetesDeploy configs: 'reactApplication.yml', kubeConfig: [path: ''], kubeconfigId: 'Kubernetes_Cluster', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
            }
        }
    }
}
