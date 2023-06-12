pipeline {
    agent { label 'myagent' }
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh '''
                                docker login -u ${USERNAME} -p ${PASSWORD}
                                docker build -t ahmadesmailshata/portfolio:v${BUILD_NUMBER} .
                                docker push ahmadesmailshata/portfolio:v${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > ../build.txt
                            '''
                        }
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                script {
                       
                            sh '''
                                export BUILD_NUMBER=$(cat ../build.txt)
                                export check=$(helm list | grep "my-release")
                                if [ -z $check ]
                                then
                                    helm install my-release ./my-chart/ --values ./my-chart/dev-values.yaml --set image.tag=${BUILD_NUMBER}
                                else
                                    helm upgrade my-release ./my-chart/ --values ./my-chart/dev-values.yaml --set image.tag=${BUILD_NUMBER}
                                fi

                            '''
         
                    }
            }
        }
    }
}
