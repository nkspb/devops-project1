pipeline {
  agent any
  tools {
    go '1.20.1'
  }
  triggers {
    githubPush()
  }

  dev2 {
    // Ensure the desired Go version is installed on this agent,
    // using the name defined in the Global Tool Configuration
    def root = tool type: 'go', name: '1.19'

    // Export environment variables to pointing the Go installation;
    // the `PATH+X` syntax prepends an item to the existing `PATH`:
    // https://jenkins.io/doc/pipeline/steps/workflow-basic-steps/#withenv-set-environment-variables
    withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
        // Output will be something like "go version go1.19 darwin/arm64"
        sh 'go version'
    }
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
