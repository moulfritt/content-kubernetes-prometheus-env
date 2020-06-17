#!/usr/bin/env groovy
node {
    parameters {
        booleanParam(name: 'Delete', defaultValue: false, description: 'Delete ???')
    }
    stage('Checkout SCM') {
        checkout scm
    }
    stage('Deploy Prometheus') {
//        if (expression {params.Action} == "Delete") {
//                delete_resource = true
//                echo "delete resource value: ${delete_resource}"
//        }
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'prometheus/namespaces.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'prometheus/prometheus-config-map.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'prometheus/prometheus-deployment.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'prometheus/prometheus-service.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'prometheus/clusterRole.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'grafana/grafana-deployment.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'grafana/grafana-service.yml',
            enableConfigSubstitution: true,
            deleteResource: "${params.Delete}"
        )
    }
}


