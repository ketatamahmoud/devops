pipeline{
  agent any
  tools {
    maven 'Maven-3.8'
  }
  stages{
    stage("build Jar"){
      steps{
        script{
          echo "building the application"
          sh "mvn clean package"
      }
    }
   }
  }
 }
