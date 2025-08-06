pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                git url:'https://github.com/Prajju1109/cicdakshat/', branch: "master"
               sh 'mvn clean install'
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
        
        stage('Debug Branch Name') {
    steps {
        script {
            echo "BRANCH_NAME env: ${env.BRANCH_NAME}"
            sh 'git branch'
            sh 'echo Current Git Branch: $(git rev-parse --abbrev-ref HEAD)'
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
