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
      stage('preparation') {
          steps {
              snApplyChanges url: "https://dev117906.service-now.com/", credentialsId: "2934736d-facb-4169-a459-01f7119eddee", appScope: "x_445116_github_ci", branchName: "${BRANCH}"
          }
      }
  }
}
