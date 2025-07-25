pipeline {
  agent any
  stages {
    stage('scm checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/kumargaurav039/maven-project.git'
      }
    }

    stage('package job') //validate, test and compile
    {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JDK_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn package'
        }
      }
    }
    stage('deploy job') 
    {
      steps {
        sshagent(['DEV_CICD']) {
          sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@3.7.69.87:/usr/share/tomcat/webapps'
        }
      }
    }
    }
  }
