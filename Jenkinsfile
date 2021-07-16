pipeline {
 agent any
   stages {
     stage('Deploy to production') {
       when { branch 'master' }
       environment {
        SERVICE_ACCOUNT_KEY     = credentials('astro-prod-service-account-key')
        REGISTRY_URL            = "registry.astro.floral.philippe.gg"
        RELEASE_NAME            = "jenkins-prod"
       }
       steps {
         script {
           sh 'docker build -t ${REGISTRY_URL}/${RELEASE_NAME}/airflow:ci-${BUILD_NUMBER} .'
           sh 'docker login ${REGISTRY_URL} -u _ -p $SERVICE_ACCOUNT_KEY'
           sh 'docker push ${REGISTRY_URL}/${RELEASE_NAME}/airflow:ci-${BUILD_NUMBER}'
         }
       }
     }

     stage('Deploy to development') {
       when { branch 'develop' }
       environment {
        SERVICE_ACCOUNT_KEY     = credentials('astro-dev-service-account-key')
        REGISTRY_URL            = "registry.astro.floral.philippe.gg"
        RELEASE_NAME            = "jenkins"
       }
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
