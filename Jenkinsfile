pipeline {
     environment {
            DOCKERHUB_CREDENTIALS = credentials('mmnassri')
        }
    agent any
    stages {

        stage('Création image Docker') {
            steps {
                sh 'docker build -t mmnassri_amsdata_2025 .'
            }
        }
         stage('Lancement de la Stack Docker-Compose') {
                    steps {
                        sh 'docker compose -f Docker-compose.yml down'
                        sh 'docker compose -f Docker-compose.yml up -d'
                    }
         }
         stage('tag and push image to dockerhub de mmnassri') {
                     steps {
                         echo "tag and push image ..."
                         sh "docker tag mmnassri_amsdata_2025 mmnassri/mmnassri_amsdata_2025"
                         sh "docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW"
                         sh "docker push mmnassri/mmnassri_amsdata_2025"
                         sh "docker logout"
                     }
                     post {
                         success {
                             echo "====++++success++++==== "
                         }
                         failure {
                             echo "====++++failed++++===="
                         }
                     }
          }
    }
}

