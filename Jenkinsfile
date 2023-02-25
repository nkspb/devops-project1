pipeline {
  agent any
  triggers {
    githubPush()
  }
  stages {
     stage('Compile app') {
       steps {
         CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ""./app/"
       }
      stage('Build container') {
        steps {
          docker build -t web-server -f "./app/Dockerfile/"
        }
      }
  }
}
}
