/* import shared library */
@Library('jenkins-shared-library')_
ignored:
  - DL3000
  - DL3022

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
                sh 'hadolint \${WORKSPACE}/main.go'
            }
        }
    }
    post {
    always {
       script {
         /* Use slackNotifier.groovy from shared library and provide current build result as parameter */
         clean
         slackNotifier currentBuild.result
     }
    }
    }
}
