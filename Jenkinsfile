pipeline {
  agent any

  stages {
    stage('Clone Repo') {
      steps {
        echo '🔄 שולפת את הקוד מה־Git...'
        checkout scm
      }
    }

    stage('Run Ansible Playbook') {
      steps {
        echo '🚀 מריצה את Playbook שמתקין Docker ומריץ קונטיינר'
        sh 'ansible-playbook -i inventory.ini install_docker.yml --ask-become-pass'
      }
    }
  }
}
