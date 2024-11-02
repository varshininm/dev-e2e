pipeline {
    agent{
         label "agent"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
        
    }
    environment {
        APP_NAME = "complete-dev-e2e"
        RELEASE = "1.0.0"
        DOCKER_USER = "varshininm"
        DOCKER_PASS = "dockerhub"
        ARTIFACTORY_REGISTRY = "https://varshininm1012.jfrog.io/docker-local"


        IMAGE_NAME = "${ARTIFACTORY_REGISTRY}/${DOCKER_USER}/${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"

    }
    stages{
        stage("Clean the workspace"){
            steps {
                cleanWs()
            }
        }
  
        stage("Checkout from SCM"){
            steps {
                git branch: 'master', credentialsId: 'github', url: 'https://github.com/varshininm/dev-e2e.git'
            }
        }

        stage("Build the code"){
            steps {
                sh "mvn clean package"
            }
        }
        stage("Test the code"){
            steps {
                sh "mvn test"
            }
        }


        // stage("Build and Push the docker image"){
        //     steps {
        //         script{
        //             withDockerRegistry('', DOCKER_PASS){
        //                 docker_image = docker.build"${IMAGE_NAME}"

        //             }
        //             withDockerRegistry('', DOCKER_PASS){
        //                 docker_image.push("${IMAGE_TAG}")
        //                 docker_image.push('latest')
        //             }
        //         }
                
        //     }
        // }

        
        stage("Build and Push the docker image to JFrog"){
            steps {
                script{
                    withDockerRegistry(credentialsId: 'JFROG_CREDENTIALS_ID', url: "${ARTIFACTORY_REGISTRY}"){
                        docker_image = docker.build("${IMAGE_NAME}")
                        docker_image.push("${IMAGE_TAG}")

                    }
                   
                }
                
            }
        }

        // stage("SonarQube Analysis"){
        //     steps {
        //         withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token'){
        //             sh "mvn sonar:sonar"

        //         }
                
        //     }
        // // }
        // stage("SonarQube Analysis"){
        //     steps {
        //         waitForQualityGate(abortPipeline: false ,  credentialsId: 'jenkins-sonarqube-token')




        //        }
                
        //     }
        }
    }

