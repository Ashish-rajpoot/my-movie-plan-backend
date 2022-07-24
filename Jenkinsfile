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
//         stage('docker compose') {
//             steps {
//                 sh "docker-compose up"
//             }
//         }
//         stage('docker build') {
//             steps {
//                 sh "docker build -t my-movie-plan ."
//             }
//         }

// stage('Docker Build Stage') {
//             steps {
//                 echo '::::: Hello, Docker Build stage  :::::'
//                 sh 'docker image build -t my-movie-plan .'                              
//             }
//         } 
//         stage('Tag docker image'){
//             steps {
//                 sh 'docker tag my-movie-plan-backend ashish142/my-movie-plan-backend:1.0.0'
//             }          
//         }
//         stage('Push docker image'){
//             steps {
//                 sh 'sudo docker push ashish142/my-movie-plan-backend:1.0.0'
//             }          
//         }
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
                 docker container run --restart always --name my-movie-plan-backend --link mysql-my-movie-plan -p 5555:5555 -d my-movie-plan-backend:1.0
            '''
//             docker container run --restart always --name planmoviebackend -p 5555:5555 -d planmoviebackend
//                  sh "docker run -p 5555:5555 --name my-movie-plan-backend --link mysql-my-movie-plan -d my-movie-plan-backend:1.0"
             }
        }
    }
}
