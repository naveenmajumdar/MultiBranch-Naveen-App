pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: node
            image: node:16-alpine3.12
            command:
            - cat
            tty: true
        '''
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
          sh ' echo Hello World created by naveen > hello.txt'
          sh ' echo adding next line to creat PR >> hello.txt'
          sh ' echo adding next line to creat PR on Main branch >> hello.txt'
          sh 'ls -last'
        }
        container('node') {
          sh 'npm version'
          sh 'cat hello.txt'
          sh 'ls -last'
        }
      }
    }
  }
}