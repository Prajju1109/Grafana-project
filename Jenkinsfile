pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/Prajju1109/Grafana-project.git'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with prajwal'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with prajwal'){
            steps{
                sh 'mvn test'
            }
        }
        
        stage('package with prajwal'){
            steps{
                sh 'mvn package'
            }
        }
    
        stage('run dockerfile'){
          steps{
               sh 'docker build -t primage1 .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8085:8085 --name cont01 primage1'
            
        }   
    }
}
}
