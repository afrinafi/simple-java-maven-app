pipeline{
    agent any 
    tools{
        maven 'maven-3'
    }
    stages{
        stage("build"){
            script{
                sh 'mvn install'
            }
        }
    }
    
}
    