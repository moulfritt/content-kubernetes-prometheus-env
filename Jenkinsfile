#!/usr/bin/env groovy
delete_resource = true


pipeline {
    agent any
    parameters {
        choice(name: 'Action', choices: ['Deploy', 'Delete'], description: "What do you want ?")
    }
    stages {
        stage('Deploy Prometheus') {
            steps {
                if (expression {params.Action} == "Delete") {
                        delete_resource = true
                        echo "delete resource value: ${params.Action}"
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
