pipeline {
    agent any
    stages {
        stage('git repo clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Ashish-rajpoot/my-movie-plan-backend.git'
            }
        }
        stage('clean') {
            steps {
                sh "mvn clean"
            }
        }
        stage('package') {
            steps {
                sh "mvn package"
            }
        }
        stage('docker run') {
             steps {
                  echo 'Hello, Docker Deployment.'
                sh '''
                 (if  [ $(docker ps -a | grep angular-my-movie-plan | cut -d " " -f1) ]; then \
                        echo $(docker rm -f angular-my-movie-plan); \
                        echo "---------------- successfully removed angular-my-movie-plan ----------------"
                     else \
                    echo OK; \
                 fi;);
                 docker container run --restart always --name my-movie-plan-backend --link mysql-my-movie-plan -p 5555:5555 -d my-movie-plan-backend
            '''
             }
        }
    }
}
