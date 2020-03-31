/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {
        stage('Check docker-compose syntax') {
            agent { docker { image 'docker/compose' } }
            steps {
                sh 'docker-compose -f \${WORKSPACE}/docker-compose.yml config'
            }
        }
        stage('Check Dockerfile syntax') {
            agent { docker { image 'hadolint/hadolint' } }
            steps {
                sh 'hadolint \${WORKSPACE}/Dockerfile'
            }
         }
         stage('Check Gofile syntax') {
            agent { docker { image 'cytopia/golint' } }
            steps {
                sh 'cytopia/golint run \${WORKSPACE}/config.go'
            }
         }
      }
   }
