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
                        withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                            sh '''
                                export BUILD_NUMBER=$(cat ../build.txt)
                                export check=$(helm list | grep "my-app-release")
                                if [ -z $check ]
                                then
                                    helm install my-app-release ./my-chart/  --set image.tag=${BUILD_NUMBER}
                                else
                                    helm upgrade my-app-release ./my-chart/  --set image.tag=${BUILD_NUMBER}
                                fi

                            '''
                        }
                    }
            }
        }
    }
}
