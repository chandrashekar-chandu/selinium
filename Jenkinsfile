// pipeline {
//     agent any

//     stages {

//         stage('Checkout from GitHub') {
//             steps {
//                 git branch: 'main',
//                     url: 'https://github.com/chandrashekar-chandu/selinium.git'
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 bat 'npm install'
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 bat '''
//                 docker build -t my-k8s-app:%BUILD_NUMBER% .
//                 docker tag my-k8s-app:%BUILD_NUMBER% chandu7521/my-k8s-app:latest
//                 '''
//             }
//         }

//         stage('Push Docker Image') {
//             steps {
//                 bat 'docker push chandu7521/my-k8s-app:latest'
//             }
//         }

//         stage('Start Minikube if not running') {
//             steps {
//                 bat '''
//                 minikube status | findstr "Running"
//                 IF %ERRORLEVEL% NEQ 0 (
//                     echo Starting Minikube...
//                     minikube start --driver=docker --memory=2048 --cpus=2
//                 )
//                 '''
//             }
//         }

//         stage('Deploy to Kubernetes') {
//             steps {
//                 bat '''
//                 minikube kubectl -- apply -f k8s\\deployment.yaml
//                 minikube kubectl -- apply -f k8s\\service.yaml
//                 minikube service my-k8s-app-service
//                 '''
//             }
//         }
//     }
// }



pipeline {
    agent any

    stages {
        stage('Start App') {
            steps {
                bat '''
                start /B npm start
                timeout /t 5
                '''
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
    }
}