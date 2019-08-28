pipeline {
    agent any
     environment {
         //have to mention the image name  by replacing the stars
        DOCKER_IMAGE_NAME = "sunnynehar56/**********"
    }
    stages{
        stage('Build stage) {
            steps {
                echo 'Running build automation'
                //build script depends on maven or gradle build
                sh '**********************'
                archiveArtifacts artifacts: '**********.zip'
            }
        }
        stage('Build docker image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    docker_image = docker.build(DOCKER_IMAGE_NAME)
                    docker_image.inside {
                        //we are running a small test to check if everything working fine.
                        sh 'echo Hello,world'
                    }
                }
            }
        }
        stage ('push Docker image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    //take the docker id from the jenkins after saving docker hub credentials
                    docker.withRegistry('https://registry.hub.docker.com', '**************') {
                        docker_image.push("${env.BUILD_NUMBER}")
                        //pushing the latest tag image as well if needed
                        docker_image.push("latest")
                    }
                }
            }
        }
        stage('DeployToProduction) {
            when {
                branch 'master'
            }
            steps{
                input 'Deploy to Production'
                //here milestone make sure that older build will never be allowed to pass thru.
                milestone(1)
                kubernetesDeploy(
                    //take the kubeconfig id from the jenkins after saving kube_config credentials
                    // id should be same what ever we have given over in jenkins
                    kubeconfigId: '****************',
                    configs: 'have-to-put-an-yaml-file-in-here.yml',
                    enableConfigSubstitution: true 
                )
            }
        }
    }
}