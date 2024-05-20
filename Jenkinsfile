pipeline {
	agent any

    environment {
		DOCKERHUB_CREDENTIALS=credentials('DockerhubID')
	}
	stages {
		stage("GitHub Checkout") {
			steps {
				git branch: 'main', url: 'https://github.com/alfredrozay1/Jenkins-With-Docker-Project.git'
			}
		}

		stage("Docker Build") {
			steps {
				sh 'docker image build -t alfredrozay/alfred-image .'
			}
		}

		stage("Authenticate to DockerHub") {
			steps {
				sh  'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
				echo 'Login complete...'
			}
		}

		stage("Tag Image and Push to DockerHub") {
			steps {
				echo 'tagging...'
				sh "docker tag alfredrozay/alfred-image docker.io/alfredrozay/alfred-new-app:$BUILD_ID"
				sh "docker push docker.io/alfredrozay/alfred-new-app:$BUILD_ID"
			}
		}

		stage("Logout") {
			steps{
				sh 'docker logout'
				echo 'Logout successful!'
			}
		}

	}

}