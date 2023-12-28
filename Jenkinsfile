pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        script{
                def mvnHome = tool name: 'MAVEN_HOME', type: 'maven'
                sh "${mvnHome}/bin/mvn package"
        }
      }
    }
    stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build -t cicd-poc-jenkins-ansible"
                       sh "docker tag cafe-shop janakiraman276/cafe-shop:$BUILD_NUMBER "
                       sh "docker push janakiraman276/cafe-shop:$BUILD_NUMBER "
                    }
                }
            }
        }
    }
}

