pipeline{
    agent any
    stages{
        stage("sonar quality check"){
            agent{
                docker {
                    image 'openjdk:11'
                }
            }
            steps{
                echo "========executing A========"
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        // some block
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                    timeout(time:1, units:"HOUR"){
                        def sq=waitForQualityGate()
                        if(sq.status!="OK"){
                            error "Pipeline aborded due to quality gate failure ${sq.statau}"
                        }
                    }
                }
            }            
        }
    }    
}