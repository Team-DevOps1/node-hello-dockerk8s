pipeline{
    agent any
    stages{
        stage("Checkout code"){
            steps{
                git credentialsId: 'mygit', url: 'https://github.com/Team-DevOps1/node-hello-dockerk8s.git'
                echo "Git Checkout done"
            }
        }
        stage("Create Docker Image"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'pass', usernameVariable: 'user')]) {
    // some block
    sh """
    docker build -t sb346/mydocnode .
    echo $pass | docker login -u $user --password-stdin
    docker push sb346/mydocnode
    """
                 }
            }
        }
        stage("Deployment And Service"){
            steps{
                withCredentials([file(credentialsId: 'kubernetes', variable: 'k8s')]) {
    // some block
    sh """
    export KUBECONFIG=$k8s
    kubectl apply -f deploy.yaml
    kubectl apply -f service.yaml
    """
                }
            }
        }
    }
}
