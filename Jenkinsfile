pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    stages{
       stage('Building image') {
      steps{
         script {  
            app = docker.build("gcr.io/int-devops-cloud-0423/nginxtst")
         }
        }
       }   
       stage('Deploy Image') {
      steps{
         script {  
            docker.withRegistry('https://gcr.io', 'gcr:int-devops-cloud-0423') {
              app.push("${env.BUILD_NUMBER}")
              app.push("latest")
            }
         }
        }
       }  
    }   
}    
