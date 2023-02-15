env.DOCKER_REGISTRY = 'ikhsannugs'
env.DOCKER_IMAGE_NAME = 'sosmed'
env.BRANCH_NAME = 'master'
pipeline {
  agent any 
    stages {
      stage('Git Check') {
        steps{
          sh "ls"
          sh "git --version"
          echo "Deployment TO ${BRANCH_NAME}" 
        }
      }
      stage('Build Docker Image') {
        steps{
          sh "docker build -t $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME-$BRANCH_NAME:${BUILD_NUMBER} ."
        }
      }
      stage('Build Push Image') {
        steps{
          sh "docker push $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME-$BRANCH_NAME:${BUILD_NUMBER}"
        }
      }
      stage('Deploy to Server') {
        steps{
          sh "sed -i "s+DOCKER_NAME+$DOCKER_REGISTRY/$DOCKER_IMAGE_NAME-$BRANCH_NAME:${BUILD_NUMBER}+g" cicle-be-staging-deployments.yaml"
          sh "docker push $DOCKER_REGISTRY/$DOCKER_IMAGE_NAME-$BRANCH_NAME:${BUILD_NUMBER}"        
        }
      }
    }
}
