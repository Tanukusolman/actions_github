pipeline{
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('checkout') {
            steps{
            git credentialsId: '48077546-c2f7-493f-86d1-81b6d6ca9efe', url: 'https://github.com/gabrielf/maven-samples.git'
            }
        }
        stage("Env Variables") {
            steps {
                sh "printenv | sort"
            }
        }
        stage("Env Variable") {
            steps {
                echo "The build number is ${env.BUILD_NUMBER}"
                echo "You can also use \${BUILD_NUMBER} -> ${BUILD_NUMBER}"
                sh 'echo "I can access $BUILD_NUMBER in shell command as well."'
            }
        }
        
        stage('build'){
            steps{
                sh 'mvn clean install -f pom.xml'
            }
        }
        //stage('Download') {
           // steps {
              //  sh 'echo "artifact file" > pom.xml'
          //  }
       // }
        stage('archieving'){
            steps{
                archiveArtifacts artifacts: 'pom.xml'
            }
        }
        stage ('success'){
            steps {
                script {
                    currentBuild.result = 'SUCCESS'
                }
            }
        }
        stage('mail'){
           steps{
               mail bcc: 'akki2483@gmail.com', body: 'HI team, this is for build testing process.', cc: 'lohita.tirunagari@gmail.com', from: '', replyTo: '', subject: 'Jenkins bob failure or success', to: 'tanukusunny11@gmail.com'
            }
        }
    }
    post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "pravalikareddydungi6@gmail.com,akki2483@gmail.com,lohita.tirunagari@gmail.com",
                sendToIndividuals: true])
        }
    }
}
