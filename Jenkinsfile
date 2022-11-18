
pipeline{
  agent any
  tools {
    maven 'Maven'
  }

  stage("build Jar"){
    steps{
      script{
        echo "building the application"
        sh "mvn clean package"
      }
    }
  }

  stage("test"){
    steps{
      echo "testing application"
    }
  }
  stage("deploy"){
    steps {
      echo "deploying app"
    }
  }
}
