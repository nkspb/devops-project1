
//   node {
//     // Ensure the desired Go version is installed on this agent,
//     // using the name defined in the Global Tool Configuration
//     def root = tool type: 'go', name: '1.20.1'

//     // Export environment variables to pointing the Go installation;
//     // the `PATH+X` syntax prepends an item to the existing `PATH`:
//     // https://jenkins.io/doc/pipeline/steps/workflow-basic-steps/#withenv-set-environment-variables
//     withEnv(["GOROOT=${root}", "PATH+GO=${root}/bin"]) {
//         // Output will be something like "go version go1.19 darwin/arm64"
//         sh 'go version'
//     }
// }

pipeline {
  agent {label 'dev2'}
  tools {
    go '1.20.1'
  }
  environment {
        GO111MODULE = 'auto'
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
        sh "cd ./app; CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main '.'"
      }
    }
        stage('Build container') {
        steps {
          sh "whoami"
          sh "cd ./app; docker build -t web-server -f Dockerfile ."
        }
     }
  }
}
