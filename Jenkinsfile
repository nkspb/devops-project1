pipeline {
  agent any
  triggers {
    githubPush()
  }
  stages {

     stage('Compile app') {
       steps {
        bash "CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main './app/'"
        // echo test1
       }
     }

      stage('Build container') {
        steps {
        bash "docker build -t web-server -f './app/Dockerfile/'"
        }
      }

  }
}