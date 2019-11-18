pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.2.0'
    BG = "private"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          bat "mvn test"
      }
    }

     stage('CloudHub Deployment') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'test-cicd-dev'
      }
      steps {
            bat 'mvn -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    }
  }
}
