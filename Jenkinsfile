pipeline {
    agent any
    tools {
        nodejs ('node21')
    }
    
    environment {
        SCANNER_HOME= tool('sonar-scanner')
    }

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/gspvsr/3-Tier-Full-Stack.git'
            }
        }
    
        stage('Install PackageDependencies') {
            steps {
                sh "npm install"
            }
        }
    
   
        stage('Unit Test') {
            steps {
                echo 'nmp test'
            }
        }
    

        stage('Trivy FS Scan') {
            steps {
                sh "trivy fs --format table -o fs-report.html ."
            }
        }
    

        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonar-scanner') {
                    sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Campground -Dsonar.projectName=Campground"
                }   
            }
        }
    

        stage('Build build & tag') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cre', toolName: 'docker') {
                        sh "docker build -t gspvsr/campa:latest ."
                    }
                }
            }
        }
    

        stage('Trivy Image Scan') {
            steps {
                sh "trivy image --format table -o fs-report.html gspvsr/camp:latest"
            }
        }
    
        stage('docker push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cre', toolName: 'docker') {
                        sh "docker push gspvsr/campa:latest"
                    }
                }
            }
        }
    
        stage('Deploy on K8') {
            steps {
                script {
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'eks-spot-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://F75C295016B043FFA79EBCD0A6D9640F.gr7.us-east-1.eks.amazonaws.com']]) {
                        sh "kubectl apply -f dss.yml"
                        sleep 60
                    }
                }
            }
        }
        stage('Verify the Deployment') {
            steps {
                script {
                    withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'eks-spot-cluster', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://F75C295016B043FFA79EBCD0A6D9640F.gr7.us-east-1.eks.amazonaws.com']]) {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                    }
                }
            }
        }
    }
}

