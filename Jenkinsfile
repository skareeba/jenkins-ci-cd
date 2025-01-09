pipeline {
    agent {
        node {
            label 'jenkins_slave_node'
        }
    }
    stages {
        stage("checkout Code") {
            steps {
                git url:'https://github.com/nomanshaikh07/Jenkins_AVD.git', branch:'main'
            }
        }
             stage("Build Docker image") {
            steps {
                sh 'docker build -t myimage .'
            }
        }
        stage('Add tag and Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker tag myimage $DOCKER_USERNAME/myimage'
                    sh 'docker push $DOCKER_USERNAME/myimage'
                }   
            }
        }
        stage('Deploy application to kubernetes') {
            steps {
                sh 'kubectl delete deployment my-deployment'
                sh 'kubectl apply -f my-deployment.yml'
            }
        }
           }
}




