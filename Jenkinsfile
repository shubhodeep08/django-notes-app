pipeline{
    agent {
        label "jenkins-agent2"
    }
    triggers {
        githubPush()
        pollSCM('H/30 * * * *')
    }
    stages{
        stage('cloning code from github')
        {
            steps
            {
                git url: 'https://github.com/shubhodeep08/django-notes-app.git',branch: 'main'
            }
        }
        stage("building for the dev branch"){
            when{
                branch "main"
            }
            steps{
                sh "docker-conpose -f Dockerfile up -d"
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
