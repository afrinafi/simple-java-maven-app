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
                        -Dsonar.host.url=http://172.31.18.76:9000 \
                        -Dsonar.login=sqp_03fdc91912927e09e37fca43ffb22f4076233c5b"
    
                    }
                }
            }

        }
        stage("upload artifact"){
            steps{
               sh 'mvn -s settings.xml deploy'
            }
        }
        

    }

}   