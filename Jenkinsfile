node {
    stage('Clone repository') {
        git branch: 'main', credentialsId: '2a672bb5-364d-49cd-af60-aa923c02d5b4', url: 'https://github.com/Lstar974/pipeline.git'
    }

    stage('Build image') {
        dockerImage = docker.build("lstar974/pipeline")
    }

    stage('Push image') {
        withDockerRegistry(credentialsId: '2d03ed10-ad94-4ea2-98c5-5ad4fe9eea5b') {
            dockerImage.push()
        }
    }

    stage('Ansible') {
        ansiblePlaybook credentialsId: 'ssh', disableHostKeyChecking: true, inventory: 'hosts.yml', playbook: 'playbook.yml', compose: 'docker-compose.yml'
        withDockerRegistry(credentialsId: '2d03ed10-ad94-4ea2-98c5-5ad4fe9eea5b') {
        }
    }
}
