pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/Anik-git96/maven-project.git'
      }
    }
    stage('package job') {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn package'
        }
      }
    }
    stage('deploy the job') {
      steps{
        sshagent(['tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pr1/webapp/target/webapp.war ec2-user@3.7.69.128:/usr/share/tomcat/webapps'
        }
      }
    }

    /*stage('create docker image') {
      steps {
        sh 'docker build -t e31531469/ethans954:latest .'
      }
    }



    stage('push docker image to dockerhub') {
      steps {
        
        withDockerRegistry(credentialsId: 'DockerHubCredentials', url: 'https://index.docker.io/v1/') {
            
                sh 'docker push e31531469/ethans954:latest'
            
        }
      }*/
    }
  }

