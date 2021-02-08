pipeline {
		agent any
		environment {
            /* repository in Dockerhub */        
			DOCKER_HUB_REPO = "karinegh18/casestudy"
			/* this should be configured in jenkins manage credentials */
			//REGISTRY_CREDENTIAL = "dockerhub"
		}
		stages {
			stage('Clean workspace'){
				steps{
					script{
						sh 'rm -rf $PWD/cicd'						
					}
				}
			}
			stage('Cloning our Git'){
				steps {
					script{
						sh 'git clone https://github.com/Kari-sad/cicd.git' 
					}		
				}
			}
			stage('Building new image ') {
				steps {
					script {
						sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
						sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER'
						echo "image buit successfuly"
					}
				}	
			}
		}
	}

