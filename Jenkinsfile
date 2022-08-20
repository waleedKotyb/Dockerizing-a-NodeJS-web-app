pipeline {
    agent any

    stages {
        stage('prep') {
            steps {
                git url="https://github.com/waleedKotyb/Dockerizing-a-NodeJS-web-app.git" , branch="main"
            }
        }
        
        
        stage('build') {
            steps {
                sh "docker build . -f Dockerfile -t jconnect/nodeapp:v1"
            }
        }

        stage('artifact') {
            steps {

                withCredentials([usernamePassword(credentialsId: 'Docker-Hub', passwordVariable: 'pass', usernameVariable: 'hubuser')])   
                {
                    sh "docker login -u ${hubuser} -p ${pass}"
                    sh "docker push jconnect/nodeapp:v1"
                }
             
            }
        }

        stage('Deploy') {
            steps {
                    sh "docker run -d -p 5050:8080 jconnect/nodeapp:v1"
             
            }
        }


    }
}
