pipeline {
    agent any
    stages {
        stage("Checkout") {
            steps {
                bat "dir"
                git branch:'main', url: 'https://github.com/wieczoreksdev/course3-jenkins-gs-spring-petclinic'
                bat "dir"    
            }
        }
    
        stage("Build") {
            steps {
                echo "Simulating build step..."
                bat "./mvnw package"
            }
        }
        
        stage("capture") {
            steps {
                archiveArtifacts '**/target/*.jar'
            }
        }
        
        stage("tests results"){
            steps {
                junit '**/target/surefire-reports/TEST*.xml'
            }
        }
        
        stage("code coverage"){
            steps {
            jacoco()
            }
        }
    }
    post {
        always {
            emailext body: '${env.BUILD_URL}', recipientProviders: [developers()], subject: 'test', to: 'test'
        }
    }
}
