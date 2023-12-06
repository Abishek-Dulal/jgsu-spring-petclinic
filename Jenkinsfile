pipeline{
    agent any
    
    stages{
        
        stage("checkout"){
            steps{
               git branch:"main" , url:"https://github.com/Abishek-Dulal/jgsu-spring-petclinic.git"    
            }
        }
        
        stage("build"){
            steps{
               sh "./mvnw package"
            }
        }
        
        stage("capture"){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'        
            }
        }
        
        
    }
    
    post{
        always{
            emailext body: "${env.BUILD_URL}\${currentBuild.absoluteUrl}",
                to:"always@foo.bar",
                recipientProviders: [buildUser(), developers()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] "    
        }
        
    }
    
    
    
}

