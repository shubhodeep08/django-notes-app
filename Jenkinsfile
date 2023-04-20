pipeline{
  agent {label "jenkins-agent2"}
  stages{
    stage('Clone the code here'){
      git url: "https://github.com/shubhodeep08/django-notes-app.git", branch: "dev"
    }
    stage("build and run the app"){
//       This will stop any running container
      sh "docker-compose down"
//       This will run the application
      sh "docker-compose up" 
    }
  }
}
