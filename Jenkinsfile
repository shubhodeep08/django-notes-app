pipeline{
    agent {
        label "jenkins-agent2"
    }
    triggers {
        githubPush()
        pollSCM('H/30 * * * *')
    }
    stages{

        stage("building for the dev branch"){
            when{
                branch "dev"
            }
            steps{
                sh "docker-conpose -f docker-compose-dev.yml up -d"
            }
        }
        stage("running app for testing branch"){
            when{
                branch "testing"
            }
            steps{
                sh "docker-compose -f docker-compose-testing up -d"
            }
        }

    }
}