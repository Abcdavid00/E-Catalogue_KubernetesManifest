node {
    
  def app

  stage('Clone repository') {
    checkout scm
  }

  stage('Update Gateway-Deployment.yaml') {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'git config user.name ${GIT_USERNAME}'
        sh 'cat Gateway-Deployment.yaml'
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/gateway.*+harbor.abcdavid.top/e_catalogue/gateway:${IMAGE_VERSION}+g" Gateway-Deployment.yaml'
        sh 'cat Gateway-Deployment.yaml'
      }
    }
  }
  stage("Update UsersMS-Deployment.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'git config user.name ${GIT_USERNAME}'
        sh 'cat UsersMS-Deployment.yaml'
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/usersms.*+harbor.abcdavid.top/e_catalogue/usersms:${IMAGE_VERSION}+g" UsersMS-Deployment.yaml'
        sh 'cat UsersMS-Deployment.yaml'
      }
    }
  }
  stage("Commit & Push") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'git add .'
        sh 'git commit -m "Update Image Version to ${IMAGE_VERSION}\nDone by Jenkins"'
        sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/E-Catalogue_KubernetesManifest.git HEAD:main'
      }
    }
  }

}