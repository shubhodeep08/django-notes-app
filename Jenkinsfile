pipeline{
    agent {
        label "jenkins-agent2"
    }
    stages{
        stage("building for the dev branch"){
            when{
                branch "main"
            }
            steps{
                sh "docker-compose up -d"
            }
        }
        stage("running app for testing branch"){
            when{
                branch "dev"
            }
            steps{
                sh "docker-compose -f docker-compose-dev.yml up -d"
            }
        }

    }
}
