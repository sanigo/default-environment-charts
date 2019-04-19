pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    DEPLOY_NAMESPACE = "change-me"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
            sh 'helm init --client-only --stable-repo-url https://helm-stable.jointforce.com && jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            sh 'helm init --client-only --stable-repo-url https://helm-stable.jointforce.com && jx step helm apply'
          }
        }
      }
    }
  }
}
