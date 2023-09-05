pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Preeti3008/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t django-notes-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"DockerHub", passwordVariable:"DockerHubPass" , usernameVariable:"DockerHubUser")])
                {
                    sh "docker tag django-notes-app ${env.DockerHubUser}/django-notes-app:latest"
                    sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                    sh "docker push ${env.DockerHubUser}/django-notes-app:latest"
                }
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }

