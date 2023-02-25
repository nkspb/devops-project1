pipeline {
  agent any
  tools {
    go '1.20.1'
  }
  triggers {
    githubPush()
  }
  stages {

     stage('Initialize app modules') {
       steps {
        script {
          try {
            sh 'cd ./app; go mod init'
        // echo test1
          } 
        catch (err) {
          echo err.getMessage()
        }
       }
       }
     }

    stage("Build app") {
      steps {
        sh "CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main '.'"
      }
    }
        stage('Build container') {
        steps {
          sh "docker build -t web-server -f './app/Dockerfile/'"
        }
     }
  }
}
