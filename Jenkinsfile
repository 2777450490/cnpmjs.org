pipeline {
    agent {
        node {
            label 'nodejs'
        }
    }

    options {
        timeout(time: 1, unit: 'HOURS')
    }

    environment {
        REGISTRY = '172.20.190.3'
        DOCKERHUB_NAMESPACE = 'base-images'
        APP_NAME = 'cnpmjs'
    }
    
    parameters {
        string(name: 'TAG_NAME', defaultValue: '', description: '请输入镜像版本号！')
    }

    stages {
        stage ('拉取代码') {
            steps {
                checkout(scm)
            }
        }


        stage ('构建镜像 & 推送镜像') {
            steps {
                container ('nodejs') {
                    sh "docker build -t ${REGISTRY}/${DOCKERHUB_NAMESPACE}/${APP_NAME}:${params.TAG_NAME} ."
                    sh "docker push ${REGISTRY}/${DOCKERHUB_NAMESPACE}/${APP_NAME}:${params.TAG_NAME}"
                }
            }
        }
    }
}
