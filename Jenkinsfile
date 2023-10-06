pipeline {
    agent any
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
        DOCKER_IMAGE = "nakshatras/cicd:${BUILD_NUMBER}"
        DOCKERFILE_LOCATION = "spring-boot-app/Dockerfile"
    }

    stages {
        stage('Git checkout') {
            steps {
                echo 'checking out from Git'
                git 'https://github.com/SathuKarki/Java_application.git'
            }
        }
      stage('Build') {
            steps {
                echo 'checking out from Git'
                sh 'cd spring-boot-app && mvn clean package'
            }
        } 
       stage('Build Docker Image') {
        
            steps {
                script {
                    sh 'cd spring-boot-app && docker build -t ${DOCKER_IMAGE} .'
                   
                    }
        }
      }
      stage('Docker Push') {
    	agent any
      steps {
      	    withCredentials([usernamePassword(credentialsId: 'Docker-cred', passwordVariable: 'DockerhubPass', usernameVariable: 'DockerhubUser')]) {
            sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPass}"
        	sh "docker push ${DOCKER_IMAGE}" 
        }
      }
    	 
    }
}
}
