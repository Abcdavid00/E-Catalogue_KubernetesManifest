node {
    
  def app

  stage('Clone repository') {
    checkout scm
  }

  stage('Update API-Gateway.yaml') {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/gateway.*+harbor.abcdavid.top/e_catalogue/gateway:${IMAGE_VERSION}+g" API-Gateway.yaml'
      }
    }
  }
  stage("Update UsersMS.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/usersms.*+harbor.abcdavid.top/e_catalogue/usersms:${IMAGE_VERSION}+g" UsersMS.yaml'
      }
    }
  }
  stage("Update UserInfoMS.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/userinfoms.*+harbor.abcdavid.top/e_catalogue/userinfoms:${IMAGE_VERSION}+g" UserInfoMS.yaml'
      }
    }
  }
  stage("Update ProductMS.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/productms.*+harbor.abcdavid.top/e_catalogue/productms:${IMAGE_VERSION}+g" ProductMS.yaml'
      }
    }
  }
  stage("Update ContactMS.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/contactms.*+harbor.abcdavid.top/e_catalogue/contactms:${IMAGE_VERSION}+g" ContactMS.yaml'
      }
    }
  }
  stage("Update OrderMS.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/orderms.*+harbor.abcdavid.top/e_catalogue/orderms:${IMAGE_VERSION}+g" OrderMS.yaml'
      }
    }
  }
  stage("Update FileServer.yaml") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        sh 'sed -i "s+harbor.abcdavid.top/e_catalogue/fileserver.*+harbor.abcdavid.top/e_catalogue/fileserver:${IMAGE_VERSION}+g" FileServer.yaml'
      }
    }
  }
  stage("Commit & Push") {
    script {
      withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME'), string(credentialsId: 'Github-gmail', variable: 'GIT_EMAIL')]) {
        sh 'git config --global user.email ${GIT_EMAIL}'
        sh 'git config --global user.name ${GIT_USERNAME}'
        sh 'git add .'
        sh 'git commit -m "Update Image Version to ${IMAGE_VERSION}\nDone by Jenkins"'
        sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/E-Catalogue_KubernetesManifest.git HEAD:main'
      }
    }
  }

}