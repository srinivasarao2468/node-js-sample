pipeline {
  agent {
    kubernetes {
        defaultContainer 'node'
        yaml '''
        apiVersion: v1
        kind: Pod
        spec:
            securityContext:
                fsGroup: 1000
            serviceAccountName: jenkins-agent
            containers:
            - name: node
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
workspaceVolume dynamicPVC(accessModes: 'ReadWriteOnce', requestsSize: "10Gi")
// workspaceVolume persistentVolumeClaimWorkspaceVolume(claimName: 'jenkins-slave-pvc', readOnly: false)
    }
   }
stages{
    stage('test'){
        steps{
            container('node'){
                script{
                    sh script: "npm i -g pnpm@7.11"
                    sh script: 'pnpm i --frozen-lockfile'
                    sh script: 'ls -al'
                    sh script: 'pwd'
                }

            }
        }
    }
    stage('test1'){
        steps{
        container('node'){
            script{
                sh script: 'sleep 60'
            }
        }
        }
    }
}
}