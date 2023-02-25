pipeline {
  agent any
  tools {
    go '1.20.1'
  }
  triggers {
    githubPush()
  }
  stages {

     stage('Compile app') {
       steps {
         sh "CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main './app/'"
        // echo test1
       }
     }

      stage('Build container') {
        steps {
          sh "docker build -t web-server -f './app/Dockerfile/'"
        }
      }

  }
}