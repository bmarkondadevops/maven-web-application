
pipeline {
    agent any

    tools {
        // Install the Maven version configured as "maven 3.8" and add it to the path.
        maven "Maven3.8.4"
        //sonarQubeScanner "SonarScanner"
		
    }
    environment {
        SONARQUBE_ENV = 'MySonarQube' // Name configured in Jenkins > Configure System
    }

    stages {
        stage('scm') {
            steps {
               git branch: 'dev', credentialsId: 'github-mycredential', url: 'https://github.com/bmarkondadevops/maven-web-application.git'
          }
        }
        
         stage('Clean') {
             steps {
               sh "mvn -Dmaven.test.failure.ignore=true clean"
           }
        }
  
        stage('compile') {
             steps {
                sh "mvn -Dmaven.test.failure.ignore=true compile"
                }
        }
        
        stage('package') {
             steps {
                sh "mvn -Dmaven.test.failure.ignore=true package"
                }
        }
         
      //stage('DeployToTomcat') {
            //steps {
              //deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '8b33923b-1a98-4eae-8cd5-dcbb65d8508e', path: '', url: 'http://172.29.45.87:9090/')], contextPath: 'maven-web-application', war: '**/*.war'
            //}
         //}
    
    //stage('Deploy') {
             //steps {
               // sh "mvn deploy"
                //}
        //}
        
        
        //stage('SonarQube Analysis') {
            //steps {
                //withSonarQubeEnv('MySonarQube') { 
                    //sh 'sonar-scanner'
                //}
            //}
       // }
       stage('Sonar Analysis') {
           steps {
            echo 'Sonar Analysis.....'
              withSonarQubeEnv('MySonarQube') {
                sh 'mvn clean package sonar:sonar'
              }
            }
       }
    }
  }
