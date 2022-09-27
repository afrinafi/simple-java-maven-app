pipeline{
    agent any 
    tools{
        maven 'maven-3'
    }
    stages{
        stage('build'){
        }
    }
    stage("sonar scanning"){
        steps{
            script{
                 //def scannerHome = tool name: 'mySonarScanner';
                    withSonarQubeEnv("MySonarqube"){
                        sh "${tool("mySonarscanner")}/bin/sonar-scanner \
                        -Dsonar.projectKey=simple-java-maven-app \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://private_ip_sonarqube:9000 \
                        -Dsonar.login= replace_with_your_secret_token"
                    }
            }
        }
    }
}
    