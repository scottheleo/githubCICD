
   
pipeline {
  agent any
  environment {
    APPSYSID = '3f8e3fe72f2001104099808cf699b672'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = '2934736d-facb-4169-a459-01f7119eddee'
    DEVENV = 'https://dev99253.service-now.com/'
    TESTENV = 'https://dev117906.service-now.com/'
    PRODENV = ''
    TESTSUITEID = '40a106908770011088f3ca280cbb3550'
  }
  stages {
    stage('Build') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", obtainVersionAutomatically: true, url: "${DEVENV}")
      }
    }
    stage('Test') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
      }
    }
    stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }
    }
  }
}
