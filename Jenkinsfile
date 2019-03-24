pipeline {
    agent any
    
    tools {
            maven 'MVN'
        }
stages{
        stage('Maven Build'){            
            steps {
                container('jenkins-slave') {
                    sh """
                    mvn clean package
                    """
                }                
            }
        }
        stage('Docker Build') {
        steps {
            container('docker') {
                            sh """
                            docker build . -t dtrapp-dockertrain-fwyi.eastus.cloudapp.azure.com/pipeline-${env.BUILD_ID}
                            docker login -u locast -p med11158 ee-dtr.sttproductions.de
                            docker image push dtrapp-dockertrain-fwyi.eastus.cloudapp.azure.com/pipeline:k8s-${env.BUILD_ID}
                            """
                            }
                }
        }
}
}
