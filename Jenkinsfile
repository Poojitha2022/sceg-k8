pipeline {
  agent any
  stages {
	stage("Git Checkout") {
      steps {
        sh 'git clone https://github.com/Poojitha2022/sceg-k8.git'
      }
	}
    stage("Building Docker Image") {
      steps {     
	sh 'whoami'      
        sh 'docker build -t poojitha2022/nodeapp_test .'
      }
    }
    stage("pushing to DockerHub") { 
        steps{
           withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
             sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
             sh 'docker push poojitha2022/nodeapp_test:latest'
           }
        }
     }
     stage("Deploying App to Kubernetes") {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "k8s")
        }
      }
    }
  }
}	
