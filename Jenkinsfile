pipeline{
  agent any
environment {
        IMAGE_NAME = 'akraminezarene/my-website'
        IMAGE_TAG = "${IMAGE_NAME}:${BUILD_NUMBER}"
}
stages {
  stage ('Build image') {
    steps {
      sh 'docker build -t ${IMAGE_TAG} .'
      echo 'Image built successfully'
      sh 'docker images '
    }
  } 
  stage('push image'){
    steps{
      sh 'docker push ${IMAGE_TAG}'
      echo 'Image pushed successfully'
    }
  }
}
}
