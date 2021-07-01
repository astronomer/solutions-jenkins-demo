pipeline {
 agent any
       environment {
        SERVICE_ACCOUNT_KEY     = credentials('astro-service-account-key')
        REGISTRY_URL            = credentials('astro-registry-url')
        RELEASE_NAME            = credentials('astro-release-name')
    }
   stages {
     stage('Deploy to astronomer') {
       when { branch 'master' }
       steps {
         script {
           sh 'docker build -t ${REGISTRY_URL}/${RELEASE_NAME}/airflow:ci-${BUILD_NUMBER} .'
           sh 'docker login ${REGISTRY_URL} -u _ -p $SERVICE_ACCOUNT_KEY'
           sh 'docker push ${REGISTRY_URL}/${RELEASE_NAME}/airflow:ci-${BUILD_NUMBER}'
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
