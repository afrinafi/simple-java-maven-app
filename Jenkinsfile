pipeline{
    agent any 
    tools{
        maven 'mymaven'
    }
    stages{
        stage("build"){
            steps{
                script{
                    sh 'mvn install'
                }

            }
        }
        stage("unit testing"){
            steps{
                
                sh 'mvn test'
            }
            post{
                success{
                     echo "junit testing is success,publishing report"
                     junit 'target/surefire-reports/*.xml'
                
                }
                failure{
                    echo "junit testing is failed"

                }
            }
        }
        stage("sonar"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'mysonar') {
                        sh "${tool("my sonarqube")}/bin/sonar-scanner \
                        -Dsonar.projectKey=simple-java-maven-app \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://172.31.27.2:9000 \
                        -Dsonar.login=sqp_25f7dde585f6341f3a80f67cb9affbd0631c196e"
    
                    }
                }
            }

        }
        stage("upload artifact"){
            steps{
               sh 'mvn deploy'
            }
        }
        
        

    }

}   