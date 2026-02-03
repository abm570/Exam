pipeline {
    agent any

  environment {
      IMAGE_NAME = 'amit570/react-image'
      IMAGE_TAG = 'latest'
  }

  stages {
      stage('Checkout') {
        steps {
          git branch: 'main',
              url: 'https://github.com/abm570/Exam.git'
        }
     }

    // stage('Running') {
    //     steps{
    //         sh 'npm start'
    //   }
    // }

    stage('Build docker image') {
        steps {
          sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG'
      }
    }

    stage('Credentials') {
        steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                      echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
              }
        }
    }
    
    stage('Pushing Docker image'){
        steps {
         sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
      }
    }

  }
  
}

