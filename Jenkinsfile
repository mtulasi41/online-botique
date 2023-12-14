pipeline {
    agent any
  
    environment {
            NAME = "online-botique"
            RELEASE = "v0.1.0"
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
                withVault(configuration: [disableChildPoliciesOverride: false, timeout: 60, vaultCredentialId: 'vaultCred', vaultUrl: 'http://35.154.124.179:8200'], vaultSecrets: [[path: 'botique/dockerhub', secretValues: [[vaultKey: 'username'], [vaultKey: 'password']]]]) {
			            sh 'docker login -u $username -p $password'

		            }
            }
        }
      
        stage('adservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/adservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:adservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:adservice-${IMAGE_TAG} ${IMAGE_NAME}:adservice-${RELEASE}'
                      
                      //scan image                  
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:adservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:adservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:adservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:adservice-${RELEASE}'
                     }
                }
            }
        }

      stage('checkoutservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/checkoutservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG} ${IMAGE_NAME}:checkoutservice-${RELEASE}'
                      
                      //scan image                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:checkoutservice-${IMAGE_TAG}_${SCANDATE}.html'

                      sh 'docker push ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:checkoutservice-${RELEASE}'
                     }
                }
            }
        }

      stage('currencyservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/currencyservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:currencyservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:currencyservice-${IMAGE_TAG} ${IMAGE_NAME}:currencyservice-${RELEASE}'
                      
                      //scan image
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:currencyservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:currencyservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:currencyservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:currencyservice-${RELEASE}'
                     }
                }
            }
        }

      stage('emailservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/emailservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:emailservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:emailservice-${IMAGE_TAG} ${IMAGE_NAME}:emailservice-${RELEASE}'
                   
                      //scan image                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:emailservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:emailservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:emailservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:emailservice-${RELEASE}'
                     }
                }
            }
        }

      stage('frontend-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/frontend')  {
                      sh 'docker build -t ${IMAGE_NAME}:frontend-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:frontend-${IMAGE_TAG} ${IMAGE_NAME}:frontend-${RELEASE}'
                      
                      //scan image                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:frontend-${IMAGE_TAG} > /var/tmp/result_${NAME}:frontend-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:frontend-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:frontend-${RELEASE}'
                     }
                }
            }
        }
      
      stage('loadgenerator-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/loadgenerator')  {
                      sh 'docker build -t ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG} ${IMAGE_NAME}:loadgenerator-${RELEASE}'
                      
                      //scan image
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG} > /var/tmp/result_${NAME}:loadgenerator-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:loadgenerator-${RELEASE}'
                     }
                }
            }
        }

      stage('productcatalogservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/productcatalogservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG} ${IMAGE_NAME}:productcatalogservice-${RELEASE}'
                      
                      //scan image
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:productcatalogservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:productcatalogservice-${RELEASE}'
                     }
                }
            }
        }

      stage('recommendationservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/recommendationservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG} ${IMAGE_NAME}:recommendationservice-${RELEASE}'
                      
                      //scan image                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:recommendationservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:recommendationservice-${RELEASE}'
                     }
                }
            }
        }

      stage('shippingservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/shippingservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:shippingservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:shippingservice-${IMAGE_TAG} ${IMAGE_NAME}:shippingservice-${RELEASE}'
                      
                      //scan image                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:shippingservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:shippingservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:shippingservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:shippingservice-${RELEASE}'
                     }
                }
            }
        }

       stage('paymentservice-DockerBuild-scan-push') {
            steps  {
                script {
                    dir('src/paymentservice')  {
                      sh 'docker build -t ${IMAGE_NAME}:paymentservice-${IMAGE_TAG} .'
                      sh 'docker tag ${IMAGE_NAME}:paymentservice-${IMAGE_TAG} ${IMAGE_NAME}:paymentservice-${RELEASE}'
                      
                      //scan image                      
                      sh 'trivy image --format template --template "@${TEMPLATE_LOC}" ${IMAGE_NAME}:paymentservice-${IMAGE_TAG} > /var/tmp/result_${NAME}:paymentservice-${IMAGE_TAG}_${SCANDATE}.html'
                                            
                      sh 'docker push ${IMAGE_NAME}:paymentservice-${IMAGE_TAG}'
                      sh 'docker push ${IMAGE_NAME}:paymentservice-${RELEASE}'
                     }
                }
            }
        }

      stage('CleanupImage') {
            steps {
                script {
                    sh 'docker rmi -f ${IMAGE_NAME}:adservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:checkoutservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:currencyservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:emailservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:frontend-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:loadgenerator-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:paymentservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:productcatalogservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:recommendationservice-${IMAGE_TAG}'
                    sh 'docker rmi -f ${IMAGE_NAME}:shippingservice-${IMAGE_TAG}'
                }
            }
        }
    
  stage ('Clone/pull Repo') {
           steps{
	            script {
	               if (fileExists('online-botique')) {
	  
	                   echo 'Cloned repo already exists - Pulling latest changes'
	   
	                    dir("online-botique") {
		                    sh 'git pull'
	                 }
            } else {
	            
	                  echo 'Repo does not exists - Cloning the repo'
      	            sh 'git clone -b feature https://github.com/mtulasi41/online-botique.git'
	                }
            }
        }
    } 
    stage('Update Manifest') {
        steps {
          script {
	          dir('online-botique/release') {
              
	            sh 'sed -i "s/'image: gcr.io/\google-samples/\microservices-demo/\emailservice:v0.8.1'/'image: ${IMAGE_NAME}:emailservice-${RELEASE}'/g" kubernetes-manifests.yaml'
	            sh 'cat kubernetes-manifests.yaml'
	          }
          }
        }
    }
 
 }
}
