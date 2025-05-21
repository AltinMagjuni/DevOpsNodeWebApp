pipeline {
    agent any
    stages {
        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DockerHub-altinmagjuni', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://172.21.0.2:2375
                            docker login -u $USERNAME -p $PASSWORD
                            docker push altinmagjuni/node_image
                        '''
                    }
                }
             }
        }
        stage('Trigger Render Deployment') {
                    steps {
                        script {
                            withCredentials([string(credentialsId: 'RENDERPLOY', variable: 'KEY')]) {
                                sh "curl https://api.render.com/deploy/$KEY"
                            }
                        }
                    }
                }
            }
        }
