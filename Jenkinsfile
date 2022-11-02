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
                  withCredentials([usernamePassword(credentialsId: 'dockerhub_key', passwordVariable: 'USERNAME', usernameVariable: 'PASSWORD')])
                {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    sh "docker build node_app/ -t abdo/app_image ."
                    sh "docker push abdo/app_image"
                    
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
