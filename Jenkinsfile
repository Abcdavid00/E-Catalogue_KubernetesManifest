pipeline {
    agent {
        kubernetes {
            yaml  '''
                  apiVersion: v1
                    kind: Pod
                    spec:
                        containers:
                        - name: shell
                          image: ubuntu
                          command:
                          - sleep
                          args:
                          - infinity
                  '''
        }
    }
    stages {
      stage('Update Gateway-Deployment.yaml') {
        steps {
          container('shell') {
            withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                sh 'git config user.name ${GIT_USERNAME}'
                sh 'cat Gateway-Deployment.yaml'
                sh 'sed -i "s+harbor.abcdavid.top/cicd_demo/gateway.*+harbor.abcdavid.top/cicd_demo/gateway:${IMAGE_VERSION}+g" Gateway-Deployment.yaml'
                sh 'cat Gateway-Deployment.yaml'
            }
          }
        }
      }
      stage("Update UsersMS-Deployment.yaml") {
        steps {
          container('shell') {
            withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                sh 'git config user.name ${GIT_USERNAME}'
                sh 'cat UsersMS-Deployment.yaml'
                sh 'sed -i "s+harbor.abcdavid.top/cicd_demo/usersms.*+harbor.abcdavid.top/cicd_demo/usersms:${IMAGE_VERSION}+g" UsersMS-Deployment.yaml'
                sh 'cat UsersMS-Deployment.yaml'
            }
          }
        }
      }
      stage("Commit & Push") {
        steps {
          container('shell') {
            withCredentials([usernamePassword(credentialsId: 'Abcdavid-Github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                sh 'git add .'
                sh 'git commit -m "Update Image Version to ${IMAGE_VERSION}\nDone by Jenkins"'
                sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/E-Catalogue_KubernetesManifest.git HEAD:${GIT_BRANCH}'
            }
          }
        }
      }
    }
}