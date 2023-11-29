node {
    
  def app

  stage('Clone repository') {
    checkout scm
  }

  stage('Update API-Gateway.yaml') {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'git config --global user.name ${GIT_USERNAME}'
        sh 'cat API-Gateway.yaml'
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/gateway.*+harbor.abcdavid.top/e_catalogue/gateway:${IMAGE_VERSION}+g" API-Gateway.yaml'
        sh 'cat API-Gateway.yaml'
      }
    }
  }
  stage("Update UsersMS.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'git config --global user.name ${GIT_USERNAME}'
        sh 'cat UsersMS.yaml'
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/usersms.*+harbor.abcdavid.top/e_catalogue/usersms:${IMAGE_VERSION}+g" UsersMS.yaml'
        sh 'cat UsersMS.yaml'
      }
    }
  }
  stage("Commit & Push") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'git config --global user.name ${GIT_USERNAME}'
        sh 'git add .'
        sh 'git commit -m "Update Image Version to ${IMAGE_VERSION}\nDone by Jenkins"'
        sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/E-Catalogue_KubernetesManifest.git HEAD:main'
      }
    }
  }

}