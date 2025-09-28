pipeline {

    environment {
        PROJECT_ID = "${PROJECT_ID}"
        REGISTRY_URL = "${REGISTRY_URL}"
        ARTIFACT_REGISTRY = "${ARTIFACT_REGISTRY}"
        CLUSTER_NAME = "${CLUSTER}"
        LOCATION = "${ZONE}"
    }

    agent any

    stages {
        stage("Checkout Git Branch") {
            steps {
                git([
                        url          : 'https://github.com/Shoppingcart-microservices/service-registry.git',
                        branch       : 'develop',
                        credentialsId: 'git'
                ])
            }
        }

        stage("Deploy MySQL configuration to GKE (Google k8s Engine)") {
            steps {
                step([
                        $class           : 'KubernetesEngineBuilder',
                        projectId        : env.PROJECT_ID,
                        clusterName      : env.CLUSTER_NAME,
                        location         : env.LOCATION,
                        manifestPattern  : 'k8s/',
                        credentialsId    : 'GCPproject',
                        verifyDeployments: true])
            }
        }
    }
}