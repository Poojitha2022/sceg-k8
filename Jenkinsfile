pipeline {
  agent any
  stages {
	stage("Checkout") {
      steps {
        sh 'git clone https://github.com/Poojitha2022/nodeapp_test.git'
      }
	}
    stage("Build Image") {
      steps {     
	sh 'whoami'      
        sh 'docker build -t poojitha2022/nodeapp_test .'
      }
    }
    stage("pushtoHub") { 
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
