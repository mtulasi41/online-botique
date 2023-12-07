pipeline {
    agent any
  
    environment {
            NAME = "online-botique"
            RELEASE = "1.0.0"
            IMAGE_REPO = "chtulasi"
            IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
            IMAGE_NAME = "${IMAGE_REPO}" + "/" + "${NAME}"
            SCANDATE = sh(returnStdout: true, script: 'date +%Y-%m-%d').trim()
            TEMPLATE_LOC = "/usr/local/share/trivy/templates/html.tpl"
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
                      sh 'docker build -t ${IMAGE_NAME}:adservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:adservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 0 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o adservice.json ${IMAGE_NAME}:adservice-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:adservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:adservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:adservice-${IMAGE_TAG}'
                     }
                }
            }
        }

      stage('checkoutservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/checkoutservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 0 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o checkoutservice.json ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:checkoutservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG}'
                     }
                }
            }
        }

      stage('currencyservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/currencyservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:currencyservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:currencyservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 0 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o currencyservice.json ${IMAGE_NAME}:currencyservice-${IMAGE_TAG}'
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:currencyservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:currencyservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:currencyservice-${IMAGE_TAG}'
                     }
                }
            }
        }

      stage('emailservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/emailservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:emailservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:emailservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 0 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o emailservice.json ${IMAGE_NAME}:emailservice-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:emailservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:emailservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:emailservice-${IMAGE_TAG}'
                     }
                }
            }
        }

      stage('frontend-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/frontend')  {
                      sh 'docker build -t ${IMAGE_NAME}:frontend-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:frontend-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 0 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o frontend.json ${IMAGE_NAME}:frontend-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:frontend-${IMAGE_TAG} > /var/tmp/result_${NAME}:frontend-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:frontend-${IMAGE_TAG}'
                     }
                }
            }
        }
      
      stage('loadgenerator-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/loadgenerator')  {
                      sh 'docker build -t ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 1 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o loadgenerator.json ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG}'
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG} > /var/tmp/result_${NAME}:loadgenerator-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG}'
                     }
                }
            }
        }

     

      stage('productcatalogservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/productcatalogservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 1 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o productcatalogservice.json ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:productcatalogservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG}'
                     }
                }
            }
        }

      stage('recommendationservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/recommendationservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 1 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o recommendationservice.json ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:recommendationservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG}'
                     }
                }
            }
        }

      stage('shippingservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/shippingservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:shippingservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:shippingservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 1 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o shippingservice.json ${IMAGE_NAME}:shippingservice-${IMAGE_TAG}'
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:shippingservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:shippingservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:shippingservice-${IMAGE_TAG}'
                     }
                }
            }
        }

       stage('paymentservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/paymentservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:paymentservice-${IMAGE_TAG} .'

                      //sh 'trivy image ${IMAGE_NAME}:paymentservice-${IMAGE_TAG} --no-progress --scanners vuln --exit-code 1 --severity CRITICAL --format table'
                      //sh 'trivy image -f json -o paymentservice.json ${IMAGE_NAME}:paymentservice-${IMAGE_TAG}'
                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:paymentservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:paymentservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:paymentservice-${IMAGE_TAG}'
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
        failure {
            emailext body: '''${SCRIPT, template="groovy-html.template"}''', 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Failed", 
                    mimeType: 'text/html',to: "chtulasi234@gmail.com"
            }
         success {
               emailext body: '''${SCRIPT, template="groovy-html.template"}''', 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Successful", 
                    mimeType: 'text/html',to: "chtulasi234@gmail.com"
          }      
    }
}
