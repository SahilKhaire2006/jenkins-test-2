pipeline{
    agent any

    environment{
        DOCKER_IMAGE = "nextjs-app"
        DOCKER_CONTAINER = "nextjs-container"
        EMAIL = "sahilkhaire6.6.2006@gmail.com"
        PORT = "3000"
    }
    stages{
        stage("CLONE DATA"){
            steps{
                echo "clOning data"
                git(
                    branch:"main",
                    url:"https://github.com/SahilKhaire2006/jenkins-test-2"
                )
            }        
        }

        stage("Build-docker image"){
            steps{
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage("Remove and stop container"){
            steps{
                sh '''
                    docker stop $DOCKER_CONTAINER || true
                    docker rm $DOCKER_CONTAINER || true
                '''
            }
        }
        stage("Docker container run"){
            steps{
                sh '''
                docker run -d \
                -p ${PORT}:${PORT} \
                --name $DOCKER_CONTAINER \
                $DOCKER_IMAGE
                '''
            }
        }
        stage("Send email notification"){
            steps{
                emailext(
                    subject:"Application is deployed using CICD pipeline!!",
                    body:"application is deployed and ready on http://15.207.21.19:3000",
                    to:"${EMAIL}"
                )
            }
        }
    }
}