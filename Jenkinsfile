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
                branch "main"
            }
            steps{
                sh "docker-conpose -f docker-compose.yml up -d"
            }
        }
        stage("running app for testing branch"){
            when{
                branch "dev"
            }
            steps{
                sh "docker-compose -f docker-compose-dev up -d"
            }
        }

    }
}
