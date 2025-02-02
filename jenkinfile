pipeline{
    agent {label "hitman"}
    stages{
        
        stage("clone code"){
            steps{
                echo "clonning code from github"
                git url: "https://github.com/Anujtiwari404/MERN-docker-compose-project ", branch:"main"
                echo "successfully"
            }
        }
        stage("build docker frontend"){
            steps{
                echo "docker build frontend"
                sh "pwd"
                sh "cd mern/frontend && docker build -t frontend-image ."
                echo "sucessfully"
            }
        }
        stage("build docker backend"){
            steps{
                echo "docker build backend "
                sh "pwd"
                sh "cd mern/backend && docker build -t backend-image ."
                echo "sucessfully"
            }
        }
        stage("dockerhub push frontend"){
            steps{
                echo "pushing  frontend image to dockerhub "
                withCredentials([usernamePassword(
                    'credentialsId':"Dockerhubcredd",
                  passwordVariable: "DockerhubPass",
                  usernameVariable:"DockerhubUser")]){
                    
                sh '''echo "$DockerhubPass" | docker login -u "$DockerhubUser" --password-stdin
                    docker image tag frontend-image $DockerhubUser/frontend-image 
                    docker push  $DockerhubUser/frontend-image '''
                
                
                sh '''echo "$DockerhubPass" | docker login -u "$DockerhubUser" --password-stdin
                    docker image tag backend-image $DockerhubUser/backend-image 
                    docker push  $DockerhubUser/backend-image '''
                }
                
                echo "push successfull"
            
            }
        }
        stage("docker compose"){
            steps{
                echo "docker compose"
                sh "docker-compose up --build -d "
                echo "sucessfully"
                
            }
        }
        
    }
}
