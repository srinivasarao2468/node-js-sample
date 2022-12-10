pipeline {
  agent {
    kubernetes {
        defaultContainer 'node'
        yaml '''
        apiVersion: v1
        kind: Pod
        spec:
            containers:
            - name: node16
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
              volumeMounts:
              - name: docker-run
                mountPath: /var/run
            volumes:
            - name: docker-run
              hostPath:
                path: /var/run
                type: Directory
'''    
    }
   }
stages{
    stage('test'){
        steps{
            container('node'){
                script{
                    cat /etc/shells
                }

            }
        }
    }
}
}