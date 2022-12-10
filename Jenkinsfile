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
          serviceAccountName: jenkins
          containers:
          - name: node
            image: node:16-alpine
            command:
          - sleep
          args:
          - 99d
         - name: docker
           image: docker
           resources:
             limits:
               memory: "512Mi"
               cpu: "500m"
             requests:
               memory: "256Mi"
               cpu: "250m"
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
        }
    }
}
}