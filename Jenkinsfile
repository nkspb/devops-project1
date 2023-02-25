pipeline {
  agent any
  triggers {
    githubPush()
  }
  stages {
     stage('build') {
       steps {
         CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main ./app/
         docker build -t web-server -f ./app/Dockerfile/
       }
  }
}
}
