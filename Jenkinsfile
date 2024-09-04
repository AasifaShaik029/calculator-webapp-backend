pipeline {
    environment {
        imagename = "backend"
        jenkinsProject = 'calculator-webapp-backend'
    }

    agent any

    stages {

        stage('Git Staging') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-cred', url: 'https://github.com/yashrpandit/calculator-webapp-backend.git']]])
            }
        }

        stage('Build image and Run image') {
            steps {
                sh 'sudo su - jenkins -s/bin/bash'

                // Build the Docker image
                sh 'sudo docker image build -t $imagename .'
            }
        }
        
        stage('Run image') {
            steps {
                // Clean up any existing container with the same name
                sh 'sudo docker rm -f $imagename || true'

                // Run the Docker container
                sh 'sudo docker run -p5000:5000 --restart=always --name $imagename -itd $imagename'
            }
        }
    }
}
