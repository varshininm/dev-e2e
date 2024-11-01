pipeline {
    agent{
         label "agent"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
        
    }
    stages{
        stage("Clean the workspace"){
            steps {
                cleanWs()
            }
        }
    }

    stages{
        stage("Checkout from SCM"){
            steps {
                git branch: 'main', credentialsId: 'github', url: ''
            }
        }
    }

}