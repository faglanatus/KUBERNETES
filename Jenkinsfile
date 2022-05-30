pipeline{

agent any

environment 
{


DOCKER_TAG = getDockerTag()
}
stages {

stage ('Preparation')
{
  steps{
        cleanWs()
     git credentialsId: 'GitHub', url: "https://github.com/faglanatus/kubernetes.git"
    }
      
}

/*stage ('Build')
{
  steps{
      sh 'echo No build requied for webapp.'
  }
    
}*/


stage('Build ')
{
  
  steps{

      sh "docker image build . -t kubernetes/web: ${DOCKER_TAG}  . "
  }
   
}


stage('Push Image')
{
  
  steps{
    withCredentials([string(credentialsId: 'DockerHub' , variable: 'DockerHub')])
    {sh "docker login -u natuss -p ${DockerHub}"}
    
    sh " docker push  natuss/alpineweb."
  }
   
}

stage('Deploy to minikube ')
{
     steps{
         sh "envsubst < ${WORKSPACE}/kubernetes-manifest.yaml | kubectl apply -f -"
     }
   

}

}


}

/*def getDockerTag(){

    def tag sh script: 'git rev-parse HEAD' , returnStdout : true
return tag

}*/



