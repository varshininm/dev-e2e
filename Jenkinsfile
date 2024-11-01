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
  
        stage("Checkout from SCM"){
            steps {
                git branch: 'master', credentialsId: 'github', url: 'https://github.com/varshininm/dev-e2e.git'
            }
        }
    }

}