pipeline{
    agent any 
    tools{
        maven 'maven-3'
    }
    stages{
        stage("build"){
            steps{
                script{
                    sh 'mvn install'
                }

            }
        }
        stage("sonar"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'mysonar') {
                        sh "${tool("mysonarscanner")}/bin/sonar-scanner \
                        -Dsonar.projectKey=simple-java-maven-app_pipeline \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://172.31.36.123:9000 \
                        -Dsonar.login=sqp_895d66c8093d08e3c548a6893a28ef8bcc43b5b3"
    
                    }
                }
            }

        }
        

    }

}   