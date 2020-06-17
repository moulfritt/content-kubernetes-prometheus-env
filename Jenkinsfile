#!/usr/bin/env groovy
delete_resource = true
node {
    parameters {
        choice(name: 'Action', choices: ['Deploy', 'Delete'], description: "What do you want ?")
    }
    stage('Checkout SCM') {
        checkout scm
    }
    stage('Deploy Prometheus') {
        if (expression {params.Action} == "Delete") {
                delete_resource = true
                echo "delete resource value: ${params.Action}"
        }
        echo "delete resource value: ${params.Action}"
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
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'grafana/grafana-deployment.yml',
            enableConfigSubstitution: true,
            deleteResource: "${delete_resource}"
        )
        kubernetesDeploy(
            kubeconfigId: 'kubeconfig',
            configs: 'grafana/grafana-service.yml',
            enableConfigSubstitution: true,
            deleteResource: "${delete_resource}"
        )
    }
}


