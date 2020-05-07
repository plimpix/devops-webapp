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
      parallel {
        stage('Build') {
          steps {
            sh '''RELEASE=devops-webapp_master-1.0.war
pwd
./gradlew build -PwarName=$RELEASE --info
ls -l build/libs/
cp ./build/libs/$RELEASE ./docker'''
          }
        }

        stage('P1') {
          steps {
            sh '''date
echo run parallel!!'''
          }
        }

        stage('P2') {
          steps {
            sh '''date
echo run parallel 2!!'''
          }
        }

      }
    }

    stage('Packaging') {
      steps {
        sh '''pwd
cd ./docker
docker build -t 170710/webapp1-2019:$BUILD_ID .
docker tag 170710/webapp1-2019:$BUILD_ID 170710/webapp1-2019:latest
docker images'''
      }
    }

    stage('Publish') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsID: 'ca-dockerhub', usernameVariable: 'DOCKER_USERNAME', passowrdVariable: 'DOCKER_PASSWORD')]) {
            sh '''
docker login -u="$DOCKER_USERNAME" -p="DOCKER_PASSWORD"
docker push 170710/webapp1-2019:$BUILD_ID
docker push 170710/webapp1-2019:latest
'''
          }
        }

      }
    }

  }
}