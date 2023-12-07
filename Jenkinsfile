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
                withVault(configuration: [disableChildPoliciesOverride: false, timeout: 60, vaultCredentialId: 'vaultCred', vaultUrl: 'http://3.109.49.100:8200'], vaultSecrets: [[path: 'botique/dockerhub', secretValues: [[vaultKey: 'username'], [vaultKey: 'password']]]]) {
			            sh 'docker login -u $username -p $password'

		            }
            }
        }
      
        stage('adservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/adservice')  {
                      sh 'docker build -t ${IMAGE_REPO}/${NAME}:adservice-${BUILD_ID} .'

                      sh 'trivy image ${IMAGE_REPO}/$NAME:adservice-${BUILD_ID} --no-progress --scanners vuln --exit-code 1 --severity CRITICAL --format table'
                      sh 'trivy image -f json -o adservice.json ${IMAGE_REPO}/$NAME:adservice-${BUILD_ID}'
                                            
                      sh 'docker push ${IMAGE_REPO}/${NAME}:adservice-${BUILD_ID}'
                     }
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
  
  post {
    always {
      emailext body: '''${SCRIPT, template="groovy-html.template"}''', 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_ID} - Successful", 
                    mimeType: 'text/html',to: "chtulasi234@gmail.com"
    }
  }
}
