node {   
    stage('Clone repository') {
        git branch: 'main', credentialsId: 'config', url: 'https://github.com/Lstar974/wordpress.git'
    }
    
    stage('Build image') {
       dockerImage = docker.build("lstar974/wordpress")
    }
    
    stage('Push image') {
        withDockerRegistry(credentialsId: 'dockerhub') {
        dockerImage.push()
        }
      stage('Ansible') {
      ansiblePlaybook credentialsId: 'ssh', disableHostKeyChecking: true, inventory: 'hosts.yml', playbook: 'playbook.yml'
      withDockerRegistry(credentialsId: 'dockerhub') {
        }
      }

    }    
}
