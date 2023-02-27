pipeline {
  agent {label 'dev2'}
  
  tools {
    go '1.20.1'
  }
  
  environment {
        GO111MODULE = 'auto'
        GIT_TAG = sh (
          script: 'git describe --tags --abbrev=0',
          returnStdout: true
        ).trim()
  }
  
  triggers {
    githubPush()
  }
  
  stages {
    stage("Build app") {          
      steps {
        sh "cd ./app; CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main '.'"
      }
    }
    stage('Build container') {
     steps {
      sh "whoami"
      sh "cd ./app; docker build -t go-server -f Dockerfile ."
      sh "docker image tag go-server nkom/go-server:$GIT_TAG"
     }
    }
    stage "Publish container" {
      steps {
        sh "docker login -u nkom -p JDmqT2pHbSr9eiB"
        sh "docker push nkom/go-server:$GIT_TAG"
      }
    }
    
  }
}
