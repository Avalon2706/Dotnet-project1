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
                    sh 'sudo docker --version'
                    sh 'sudo dotnet --info'
                }
            }
        }

        stage('Checkout Jenkins Upgrade3 Git Repository') {
            steps {
                script {
                    // Clone the Git repository's master branch
                    def gitRepoUrl = 'https://github.com/Avalon2706/Dotnet-project1.git'

                    checkout([$class: 'GitSCM', 
                        branches: [[name: '*/master']], 
                        userRemoteConfigs: [[url: gitRepoUrl]], 
                        extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'CloneOption', noTags: false, shallow: true, depth: 1]]
                    ])
                }
            }
        }

        stage('build and create docker image') {
            steps {
                sh 'docker build -f Dockerfile.fixed -t $IMAGE '
            }
        } 

        stage ('Pushing docker image to registry') {
            steps {
                docker.withRegistry('https://index.docker.io/','dockerhub-creds'){
                    sh 'Docker push $IMAGE'
    

        

        
            }
        }
    }
}
}
