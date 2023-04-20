pipeline{
  agent {label "jenkins-agent2"}

  properties
  (
    [
        pipelineTriggers
        (
          [
            githubPush(),
            githubPullRequest()
          ]
        )
    ]
  )

  stages{
    stage('Clone Repository') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/dev'], [name: '*/testing']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/shubhodeep08/django-notes-app.git',
                    ]]
                ])
            }
        }
    stage("cleanup"){
      steps{
        sh "docker-compose down"
      }
    }
    stage('Build') {
            parallel {
                stage('Dev Branch') {
                    steps {
                        sh 'docker-compose -f docker-compose-dev.yml build --build-arg BRANCH=dev'
                    }
                }
                stage('Testing Branch') {
                    steps {
                        sh 'docker-compose -f docker-compose-testing.yml build --build-arg BRANCH=testing'
                    }
                }
            }
        }
    stage('Run') {
            parallel {
                stage('Dev Branch') {
                    steps {
                        sh 'docker-compose up -d dev'
                    }
                }
                stage('Testing Branch') {
                    steps {
                        sh 'docker-compose up -d testing'
                    }
                }
            }
        }

  }
}
