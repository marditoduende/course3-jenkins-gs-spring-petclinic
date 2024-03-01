pipeline {
    agent any
    stages{
        stage ("checkout"){
            steps{
                git branch:'main', url: 'https://github.com/marditoduende/course3-jenkins-gs-spring-petclinic'
            }
        }
        stage("build"){
            steps{
                bat "./mvnw.cmd package"
            }
        }
        stage("capture"){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar'
                jacoco()
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
            }
        }
    }
    
    post {
        always {
            echo "Body: ${env.BUILD_URL}\n${currentBuild.absoluteUrl}"
            echo "Subject: ${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }
}
