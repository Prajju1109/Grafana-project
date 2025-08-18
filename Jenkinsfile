pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                git url:'https://github.com/Prajju1109/cicdakshat/', branch: "master"
               sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t prajju1109/image1:v1 .'
                }
            }
        }
        
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockercred', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push prajju1109/image1:v1'
                }
            }
        }
        
        
stage('Deploy to k8s') {
when{ expression {env.GIT_BRANCH == 'master'}}
            
    steps {
        script {
            kubernetesDeploy(
                configs: 'deploymentservice.yaml', // ✅ correct file name
                kubeconfigId: 'kubeconfig'
            )
        }
    }
}

    }
}
