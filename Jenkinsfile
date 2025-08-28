pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/Prajju1109/Grafana-project.git'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with akshat'){
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
               sh 'docker build -t primage11 .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 1234:8085 --name cont1 primage11'
            
        }   
    }
}
}
