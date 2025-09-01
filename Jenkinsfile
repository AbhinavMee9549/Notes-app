pipeline {
    agent any

    stages {
        stage('Git Clone') {
            steps {
                echo 'Cloning'
                git branch: 'main', url: 'https://github.com/AbhinavMee9549/Notes-app.git'
            }
        }
        
        stage('Image Building') {
            steps {
                echo 'Building...'
                sh "docker build -t notes-app ."
            }
        }
        
        stage('DockerHub') {
            steps {
                echo 'pushing to docker hub'
                withCredentials([string(credentialsId: 'dockerhub', variable: 'DOCKERHUB_TOKEN')]) {
                sh "docker tag notes-app abhi414/notes-app:latest"    
                sh """
                echo $DOCKERHUB_TOKEN | docker login -u abhi414 --password-stdin
                  """
                  sh "docker push abhi414/notes-app:latest"
                  }
                
            }
        }
        
        stage('DockerRun') {
            steps {
                echo 'container running'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
