pipeline {
    agent any
    stages {
        stage('EKS Login') {
                steps {
                    script{
                        sh """
                            aws eks update-kubeconfig --region us-east-1 --name roboshop
                        """
                    }
                }
        }
        stage ('create namespace') {
            steps{
                script {
                      sh """
                      cd helm
                      kubectl apply -f namespace.yaml

                      """
                }
            }
        }
        stage('EKS Deploy') {
            steps {
                script{
                    sh """
                        cd helm
                        helm upgrade --install catalogue -n roboshop .
                    """
                }
            }
        }

    }

    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
    }
}