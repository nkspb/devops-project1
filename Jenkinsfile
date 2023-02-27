pipeline {
  agent {label 'dev2'}
  
  tools {
    go '1.20.1'
  }
  
  environment {
        GO111MODULE = 'auto'
        TAG_NAME = "${env.BRANCH_NAME}"
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
      sh "cd ./app; docker build -t web-server -f Dockerfile ."
      sh "echo $TAG_NAME"
     }
    }
  }
}
