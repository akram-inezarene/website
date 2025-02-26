pipeline{
  agent { label 'VM2-node' } 
environment {
        IMAGE_NAME = 'akraminezarene/my-website:123'
      //  IMAGE_TAG = "${IMAGE_NAME}:${BUILD_NUMBER}"
        KUBECONFIG = credentials('kubeconfig-creds-id')
}
stages {

  stage ('login to docker hub') {
    steps {
      withCredentials ([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'USERNAME', passwordVariable:'PASSWORD')]) {
        sh 'echo ${PASSWORD} | docker login -u ${USERNAME} --password-stdin'}
        echo 'Logged in to docker hub'
    }
  }
  stage ('Build image') {
    steps {
      sh 'docker build -t akraminezarene/my-website:123 .'
      echo 'Image built successfully'
      sh 'docker images '
    }
  } 
  stage('push image'){
    steps{
      sh 'docker push akraminezarene/my-website:123'
      echo 'Image pushed successfully'
    }
  }
  stage('deploy to k3s'){
    steps{
    {
      sh 'kubectl apply -f deploy.yaml'
      echo 'Deployment done successfully'
    }
  }
}
}
