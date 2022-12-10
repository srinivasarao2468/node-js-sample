pipeline {
  agent {
    kubernetes {
        defaultContainer 'node'
        yaml '''
        apiVersion: v1
        kind: Pod
        spec:
            serviceAccountName: jenkins-agent
            containers:
            - name: node16
              image: node:16-alpine
              command:
              - sleep
              args:
              - 99d
            - name: kubectl
              image: gcr.io/cloud-builders/kubectl
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
            container('node16'){
                script{
                    CURRENT_CONTAINER=sh(script: 'node --version',
                                        returnStdout: true
                                        ).trim()
                    echo "Exec container ${CURRENT_CONTAINER}"
                }

            }
        }
    }
    stage('test1'){
        steps{
            echo "CURRENT_CONTAINER is ${CURRENT_CONTAINER}"
        }
    }
}
}