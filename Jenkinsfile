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
                            docker build . -t 34.73.159.116/pipeline-${env.BUILD_ID}
                            docker login -u locast -p med11158 34.73.159.116
                            docker image push 34.73.159.116/pipeline:k8s-${env.BUILD_ID}
                            """
                            }
                }
        }
}
}
