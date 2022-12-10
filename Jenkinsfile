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
            - name: node18
              image: node:18-alpine
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
            container('node18'){
                script{
                    sh returnStdout: true, script: 'npm install'
                }

            }
        }
    }
    stage('test1'){
        steps{
        container('node18'){
            script{
                sh returnStdout: true, script: 'npm build'
            }
        }
        }
    }
}
}