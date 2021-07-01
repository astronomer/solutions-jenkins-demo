pipeline {
 agent any
   stages {

     stage('Deploy to development') {
       when { branch 'develop' }
       environment {
        SERVICE_ACCOUNT_KEY     = credentials('astro-dev-service-account-key')
        REGISTRY_URL            = "registry.polaris.astronomerdemo.com"
        RELEASE_NAME            = "infrared-comet-4238"
       }
       steps {
         script {
           sh 'docker build -t ${REGISTRY_URL}/${RELEASE_NAME}/airflow:ci-${BUILD_NUMBER} .'
           sh 'docker login ${REGISTRY_URL} -u _ -p $SERVICE_ACCOUNT_KEY'
           sh 'docker push ${REGISTRY_URL}/${RELEASE_NAME}/airflow:ci-${BUILD_NUMBER}'
         }
       }
     }

     stage('Deploy to production') {
       when { branch 'master' }
       environment {
        SERVICE_ACCOUNT_KEY     = credentials('astro-prod-service-account-key')
        REGISTRY_URL            = "registry.polaris.astronomerdemo.com"
        RELEASE_NAME            = "planetoidal-planet-3558"
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
