pipeline {
    agent any
    tools{
        maven 'maven-3.5.0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SelmaGuedidi/devops-automation']]])
                sh 'mvn clean install'
            }
        }
         stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t selmaguedidi/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u selmaguedidi -p ${dockerhubpwd}'

}
                   sh 'docker push selmaguedidi/devops-integration'
                }
            }
        }
        
        
    }
}
