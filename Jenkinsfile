
pipeline{
  agent any
  tools {
    maven 'Maven'
  }

  stages{
    stage("increment version..."){
      steps{
        script{
          echo "incrementing version"
          sh 'mvn build-helper:parse-version versions:set \
          -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} versions:commit'
          def matcher =readFile('pom.xml') =~ '<version>(.+)</version>'
         def version =matcher[0][1]
         env.IMAGE_NAME="$version"
        }
      }
    }

  stage("build Jar"){
    steps{
      script{
        echo "building the application"
        sh "mvn clean package"
      }
    }
  }
  stage("build image"){
      steps{
        script{
          echo "building the image"
          withCredentials([usernamePassword(credentialsId :'docker_hub', passwordVariable: 'pass', usernameVariable:'user')]){
            sh "docker build -t gaston2000/maven-app:javamavenApp:${IMAGE_NAME} ."
            sh "echo $pass | docker login -u $user --password-stdin" 
            sh "docker push gaston2000/maven-app:javamavenApp:${IMAGE_NAME}"
            
          }
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
