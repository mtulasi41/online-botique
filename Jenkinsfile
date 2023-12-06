pipeline {
    agent any
  
    environment {
            NAME = "online-botique"
            IMAGE_REPO = "chtulasi"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/feature']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mtulasi41/online-botique.git']])
            }
        }
      
        stage('DockerLogin') {
            steps {
                withVault(configuration: [disableChildPoliciesOverride: false, timeout: 60, vaultCredentialId: 'vaultCred', vaultUrl: 'http://15.206.146.130:8200'], vaultSecrets: [[path: 'botique/dockerhub', secretValues: [[vaultKey: 'username'], [vaultKey: 'password']]]]) {
			            sh 'docker login -u $username -p $password'

		            }
            }
        }
      
        stage('adservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/adservice')  {
                      sh 'docker build -t ${IMAGE_REPO}/${NAME}:adservice-${BUILD_ID} .'
                      sh 'trivy ${IMAGE_REPO}/${NAME}:adservice-${BUILD_ID} --no-progress --scanners vuln  --exit-code 0 --severity HIGH,CRITICAL --format table'
                      sh 'docker push ${IMAGE_REPO}/${NAME}:adservice-${BUILD_ID}'
                     }
                }
            }
        }
        stage('checkoutservice-DockerBuild') {
            steps  {
                script {
                    dir('src/checkoutservice')  {
                        
                    sh 'docker build -t ${IMAGE_REPO}/$NAME:checkoutservice-${BUILD_ID} .'
                    // sh 'docker tag checkoutservice:v1.$BUILD_ID ${IMAGE_REPO}/$NAME:checkoutservice-${BUILD_ID}'
                    }
                    sh 'docker push ${IMAGE_REPO}/$NAME:checkoutservice-${BUILD_ID}'
                }
            }
        }
        stage('CleanupImage') {
            steps {
                script {
                    sh 'docker rmi -f $(docker images -a -q)'
                }
            }
        }
        
    }
}
