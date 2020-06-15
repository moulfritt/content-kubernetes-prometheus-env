pipeline {
    agent any
    environment {
        //be sure to replace "willbla" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "fbruslon/train-schedule"
    }
    stages {
        stage('Deploy Prometheus') {
            steps {
                step('Create Namespace') {
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/namespaces.yml',
                    enableConfigSubstitution: true
                )
                }
                step('Create ClusterRole') {
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/clusterRole.yml',
                    enableConfigSubstitution: true
                )
                }
                step('Create ConfigMap') {
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    cconfigs: 'prometheus/prometheus-config-map.yml',
                    enableConfigSubstitution: true
                )
                }
                step('Create Deployment') {
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/prometheus-deployment.yml',
                    enableConfigSubstitution: true
                )
                }
                step('Create Service') {
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'prometheus/prometheus-service.yml',
                    enableConfigSubstitution: true
                )
                }
                step('Create Namespace') {
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'train-schedule-kube.yml',
                    enableConfigSubstitution: true
                )
                }
            }
        }
    }
}
