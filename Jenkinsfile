pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/Prajwal-new/php-project.git', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t prajju1109/php-project .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push prajju1109/php-project'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 prajju1109'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 prajju1109/php-project"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.159 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.159 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
