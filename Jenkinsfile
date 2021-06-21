pipeline {
 agent any
       environment {
        $SERVICE_ACCOUNT_KEY     = credentials('astro-service-account-key')
    }
   stages {
     stage('Deploy to astronomer') {
       when { branch 'master' }
       steps {
         script {
           sh 'docker build -t registry.polaris.astronomerdemo.com/infrared-comet-4238/airflow:ci-${BUILD_NUMBER} .'
           sh 'docker login registry.polaris.astronomerdemo.com -u _ -p $SERVICE_ACCOUNT_KEY'
           sh 'docker push registry.polaris.astronomerdemo.com/infrared-comet-4238/airflow:ci-${BUILD_NUMBER}'
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
