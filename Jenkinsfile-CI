pipeline {
  agent any
  stages {
    stage('Checkout code') {
        steps {
				checkout([$class: 'GitSCM', branches: [[name: "master"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Jenkins-Github', url: "https://github.com/dockersamples/example-voting-app.git"]]])
            }
        }
    stage('Build docker images') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Push result image') {
		  steps {
			withDockerRegistry(credentialsId: 'JenkinsDockerHub', url:'') {
			  sh 'docker push gopalagarwal/result'
			  sh 'docker push gopalagarwal/vote '
			  sh 'docker push gopalagarwal/worker'
			}
		}
    }
  }
}