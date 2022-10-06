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
        stage("upload artifact"){
            steps{
               sh 'mvn -s settings.xml deploy'
            }
        }
        

    }

}   