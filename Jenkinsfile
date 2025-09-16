pipeline{
    agent any;
    
    stages{
        stage("code"){
            steps{
                git url: "https://github.com/rohaan-devops/two-tier-flask-app.git", branch: "master"
                echo "code is cloned!!"
            }
        }
        stage("build"){
            steps{
                sh "docker build -t my-app ."
                echo "docker build is done!"
            }
        }
        stage("test"){
            steps{
                echo "developer / tester will provide the test!"
            }
        }
        stage("push to Docker Hub") {
            steps {
                withCredentials([usernamePassword(credentialsId: "DockerHubCreds",
                                                  usernameVariable: "DockerHubUser",
                                                  passwordVariable: "DockerHubPass")]){
                
                sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker image tag my-app ${env.DockerHubUser}/my-app"
                sh "docker push ${env.DockerHubUser}/my-app:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d"
                echo "docker compose is used to deploy"
            }
        }
    }
}
