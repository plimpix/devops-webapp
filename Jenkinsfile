pipeline {
  agent {
    node {
      label 'agent1'
    }

  }
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/plimpix/devops-webapp.git', branch: 'master')
      }
    }

    stage('Build') {
      steps {
        sh '''whomi
date
echo $PATH
pwd
ls -la
./gradlew build --info'''
      }
    }

    stage('Publish') {
      steps {
        archiveArtifacts(artifacts: 'builds/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
      }
    }

  }
}