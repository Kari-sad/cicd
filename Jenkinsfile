pipeline {
		agent any
		environment {
            /* repository in ECR */        
			ECR_HUB_REPO = "public.ecr.aws/m8h9o2j8/flask"
			/* this should be configured in jenkins manage credentials */
			REGISTRY_CREDENTIAL = "ecr-credential"
		}
		stages {
			stage('Clean workspace'){
				steps{
					script{
						cleanWs()						
					}
				}
			}
			stage('Cloning our Git'){
				steps {
					script{
						git 'https://github.com/Kari-sad/cicd.git' 
					}		
				}
			}
			stage('Building new image ') {
				steps {
					script {
						sh 'docker image build -t $ECR_HUB_REPO:latest .'
						sh 'docker image tag $ECR_HUB_REPO:latest $ECR_HUB_REPO:$BUILD_NUMBER'
						echo "image buit successfuly"
					}
				}	
			}
			stage('Pushing image to Amazon ECR'){
				steps {
					script {
						withDockerRegistry(credentialsId: 'ecr:us-east-1:ecr-user', url: 'public.ecr.aws/m8h9o2j8/flask'){
							sh 'docker push $ECR_HUB_REPO:$BUILD_NUMBER'
							sh 'docker push $ECR_HUB_REPO:latest'
						}
						echo "Image pushed to ECR repository"
					}
				}
			}
			//stage('delete local docker image') {
			//	steps {
			//		script {
						// make sure that the Docker image is removed
			//			sh "docker rmi $ECR_HUB_REPO:latest"
			//		}
			//	}
			//}
		}	
	}
	
	

