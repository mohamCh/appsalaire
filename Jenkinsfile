 node{
     def app
      stage('Clone') {
          checkout scm
      }
      stage('SSH') {
        sh "apk add ansible sshpass"
        sh "rm -rf /root/.ssh"
        sh "echo \"192.168.56.101 app-salaire.moham.form\" > /etc/hosts"
        sh "ssh-keygen -q -t rsa -N '' -f ~/.ssh/id_rsa"
        sh "sshpass -p 'Respons11' ssh-copy-id -o stricthostkeychecking=no root@192.168.56.102"
      }
      stage('Ansible') {
        ansiblePlaybook (
            inventory: 'hosts.yaml',
            playbook: 'playbook.yaml',
            colorized: true,
            become: true,
        )
      }

}
