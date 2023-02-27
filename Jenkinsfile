TAG = sh (returnStdout: true, script: 'git fetch --tags && git tag --points-at HEAD | awk NF').trim()

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

//      stage('Initialize app modules') {
//        steps {
//         script {
//           try {
//             sh 'cd ./app; go mod init'
//           } 
//         catch (err) {
//           echo err.getMessage()
//         }
//        }
//        }
//      }

    stage("Build app") {
                
      steps {
        sh "cd ./app; CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main '.'"
      }
    }
        stage('Build container') {
        steps {
          sh "whoami"
          sh "cd ./app; docker build -t web-server -f Dockerfile ."

          sh "echo $TAG"
          
        }
     }
  }
}
