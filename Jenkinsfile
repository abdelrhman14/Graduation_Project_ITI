pipeline {
    agent any
        stages {
          stage('Build') {
            steps {
                // Get some code from a GitHub repository
                 git branch: 'main',
                    url: 'https://github.com/abdelrhman14/Graduation_Project_ITI.git'

            }
        }
        stage('continuous integration') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'dockerhub_key', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')])
                {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    cd node_app
                    sh "docker build -t app_image ."
                    sh "docker tag app_image abdelrahman1413/app_image"
                    sh "docker push abdelrahman1413/app_image"
                    echo Done
                    
                }
            }    
        }
         stage ('deployment application'){
            steps {
                sh """
                kubectl apply -f namespace.yml
                kubectl apply -f deployment.yml
                kubectl apply -f app_loadbalancer.yml

                echo Successful
            """
            }
        
        }
    }
}
