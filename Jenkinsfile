pipeline {
  agent {
    kubernetes {
        defaultContainer 'node'
        yaml '''
        apiVersion: v1
        kind: Pod
        spec:
            containers:
            - name: maven
              image: node:16-alpine
              command:
              - sleep
              args:
              - 99d
            - name: docker
              image: docker
              command:
              - sleep
              args:
              - 99d
'''    
    }
   }
stages{
    stage('test'){
        steps{
            sh "sleep 120"
        }
    }
}
}