pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/vidyagouda/php-project/'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t vidyagouda/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'vidya-docker', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push vidyagouda/akshatnewimg6july:v1'
                }
                
            }
        }
        stage("deployment"){
            steps{
                script{
                sh 'docker run -dt --name c2 -p 9000:80 vidyagouda/akshatnewimg6july:v1'
            }
            }
        }
            
    }
}
        
    
