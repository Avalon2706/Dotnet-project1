pipeline {
    agent any
    environment {
        IMAGE = "gparag27/TestProject:latest"
        }
    stages {
        stage('Verify Shell Environment') {
            steps {
                script {
                    // Get the job name and build number
                    def jobName = env.JOB_NAME
                    def buildNumber = env.BUILD_NUMBER

                    // Print the job name and build number
                    echo "Job Name: $jobName"
                    echo "Build Number: $buildNumber"

                    // Use them in shell commands
                    sh 'docker --version'
                    sh 'dotnet --info'
                    
                }
            }
        }

        stage('build and create docker image') {
            steps {
                sh 'docker build -f Dockerfile.fixed -t $IMAGE . '
            }
        } 

        stage ('Pushing docker image to registry') {
            steps {
                script {
                docker.withRegistry('https://index.docker.io/','dockerhub-creds'){
                    sh 'docker push $IMAGE'
    
                }
        

        
            }
        }
    }
}
}
