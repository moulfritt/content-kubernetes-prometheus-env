#!/usr/bin/env groovy
delete_resource = false

pipeline {
    agent any
    parameters {
        choice(name: 'Action', choices: ['Deploy', 'Delete'], description: "What do you want ?")
    }
    echo "delete resource value: ${delete_resource}"
    stages {
        stage('Deploy Prometheus') {
            steps {
                script {
                    if (${params.Action}) {
                        delete_resource = true
                        echo "delete resource value: ${delete_resource}"
                    }
                }
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/namespaces.yml',
                    enableConfigSubstitution: true,
                    deleteResource: "${delete_resource}"
                )
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/prometheus-config-map.yml',
                    enableConfigSubstitution: true,
                    deleteResource: "${delete_resource}"
                )
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/prometheus-deployment.yml',
                    enableConfigSubstitution: true,
                    deleteResource: "${delete_resource}"
                )
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/prometheus-service.yml',
                    enableConfigSubstitution: true,
                    deleteResource: "${delete_resource}"
                )
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/clusterRole.yml',
                    enableConfigSubstitution: true,
                    deleteResource: "${delete_resource}"
                )
            }
        }
    }
}
