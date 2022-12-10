pipeline {
  agent {
    kubernetes {
        defaultContainer 'node'
        yaml '''
        apiVersion: v1
        kind: pod
        metadata:
            name: jenkins-agent
        spec:
            serviceAccountName: jenkins-agent
            containers:
            - name: node
              image: node:16-alpine
              command:
              - sleep
              args:
              - 99d
            volumes:
            - name: docker-run
              hostpath:
                path: /var/run
                type: Directory
    '''           
    }
   }
stages{
    stage('test'){
        steps{
            sh "node --version"
            sh "docker --version"
            sh "helm --version"
        }
    }
}
}