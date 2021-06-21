pipeline {
 agent any
   stages {
     stage('Deploy to astronomer') {
       when { branch 'master' }
       steps {
         script {
           sh 'docker build -t registry.gcp0001.us-east4.astronomer.io/infrared-comet-4238/airflow:ci-${BUILD_NUMBER} .'
           sh 'docker login registry.gcp0001.us-east4.astronomer.io -u _ -p $SERVICE_ACCOUNT_KEY'
           sh 'docker push registry.gcp0001.us-east4.astronomer.io/infrared-comet-4238/airflow:ci-${BUILD_NUMBER}'
         }
       }
     }
   }
 post {
   always {
     cleanWs()
   }
 }
}
