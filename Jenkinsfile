pipeline {
    agent any

    tools {
        nodejs "NodeJS_20"
    }

    environment {
        // ✅ Use your working kubeconfig path
        KUBECONFIG = '/home/yarul8406/.kube/config'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Arul3011/cicd-pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    export NODE_OPTIONS="--max-old-space-size=2048"
                    npm run test -- --runInBand
                '''
            }
        }

//    stage('docker built and push'){ 
//     steps { 
//         sh ''' 
//         docker login -u arul8406 -p Arul301104@ 
//         docker build -t arul8406/jenkins-img:test . 
//         docker push arul8406/jenkins-img:test 
//         ''' 
//         }
//     }

        stage('GKE Image Rollout') {
            steps {
                sh '''
                    echo "Using kubeconfig at $KUBECONFIG"
                    kubectl get nodes

                    echo "Updating deployment image..."
                    kubectl set image deployment/frontend-deployment frontend=nginx

                    echo "Waiting for rollout to complete..."
                    kubectl rollout status deployment/frontend-deployment
                '''
            }
        }
    }

    post {
        always {
            echo "Cleaning up workspace..."
            cleanWs(deleteDirs: true)
        }
        success {
            echo "✅ Pipeline succeeded"
        }
        failure {
            echo "❌ Pipeline failed"
        }
        aborted {
            echo "⚠️ Pipeline aborted"
        }
    }
}
