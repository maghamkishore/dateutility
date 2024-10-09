pipeline {
    agent any
    stages {
        stage('preparation') {
            steps {
                echo 'Cloning the code from github'
                sh'''
                sudo rm -rf dateutility
                git clone https://github.com/Ikrao/dateutility.git
                '''
                echo 'Code cloning Completed'
            }
        }
            stage('Maven Build'){
                steps{
                    echo 'Maven Build'
                    sh'''
                    cd dateutility
                    sudo mvn clean install
                    '''
                    echo 'maven installed'
                }
            }
            stage('Build'){
              steps{
                  echo 'Image Build'
                  sh'''
                  sudo docker build -t kish24/dateutility:latest .
                  '''
                  echo 'Image Build success'
              }
            }
            stage('Docker Images'){
                steps{
                    echo 'Docker Images'
                    sh'''
                    sudo docker images
                    '''
                }
            }
            stage('Docker Push'){
                steps{
                    echo 'Image Push to dockerhub'
                    sh'''
                    sudo docker push kish24/dateutility:latest
                    '''
                }
            }
            stage('Docker Run'){
                steps{
                    echo' Image run in docker'
                    sh'''
                    sudo docker run -d -p 8081:8090 --name javaapp kish24/dateutility:latest
                    '''
                }
            }
        }
    }